---
layout: post
title: To add Oculus support to a new application (Oculus-e2
categories: Learning_Oculus_PC_SDK
tags: Oculus_PC_SDK
---



-------------------
There are three major phases when using the SDK: **setup, the game loop, and shutdown**.

**To add Oculus support to a new application**, do the following:

1. Initialize LibOVR through **ovr_Initialize**.
2. Call **ovr_Create** and check the return value to see if it succeeded. You can periodically poll for the presence of an HMD with **ovr_GetHmdDesc(nullptr)**.
3. Integrate head-tracking into your application’s view and movement code. This involves:
 - Obtaining predicted headset orientation for the frame through a combination of the **GetPredictedDisplayTime** and **ovr_GetTrackingState** calls.
 - Applying Rift orientation and position to the camera view, while combining it with other application controls.
 - Modifying movement and game play to consider head orientation.
4. Initialize rendering for the HMD.
 - Select rendering parameters such as resolution and field of view based on HMD capabilities.
         - See: ovr_GetFovTextureSize and ovr_GetRenderDesc.
 - Configure rendering by creating D3D/OpenGL-specific swap texture sets to present data to the headset.
         - See: ovr_CreateTextureSwapChainDX and ovr_CreateTextureSwapChainGL.
5. Modify application frame rendering to integrate HMD support and proper frame timing:
 - Make sure your engine supports rendering stereo views.
 - Add frame timing logic into the render loop to obtain correctly predicted eye render poses.
 - Render each eye’s view to intermediate render targets.
 - Submit the rendered frame to the headset by calling **ovr_SubmitFrame**.
6. Customize UI screens to work well inside of the headset.
7. Destroy the created resources during shutdown.
       - See: ovr_DestroyTextureSwapChain, ovr_Destroy, and ovr_Shutdown.





---
# Example Code Snippet
---
The following code **initializes LibOVR** and requests information about the available HMD.

---

```C
// Include the OculusVR SDK
	#include <OVR_CAPI.h>
	void Application()
	{
	   ovrResult result = ovr_Initialize(nullptr);
	   if (OVR_FAILURE(result))
	       return;

	   ovrSession session;
	   ovrGraphicsLuid luid;
	   result = ovr_Create(&session, &luid);
	   if (OVR_FAILURE(result))
	   {
	      ovr_Shutdown();
	      return;
	   }
		// !!! 获取HMD信息
	   ovrHmdDesc desc = ovr_GetHmdDesc(session);
	   ovrSizei resolution = desc.Resolution;

	   ovr_Destroy(session);
	   ovr_Shutdown();
	}
```

As you can see, **ovr_Initialize is called before any other API functions** and **ovr_Shutdown is called to shut down the library before you exit the program.** In between these function calls, you are free to create HMD objects, access tracking state, and perform application rendering.

In this example,** ovr_Create(&session &luid) creates the HMD**. Use the LUID returned by ovr_Create() to select the IDXGIAdapter on which your ID3D11Device or ID3D12Device is created. Finally, ovr_Destroy must be called to clear the HMD before shutting down the library.



The description of an **HMD (ovrHmdDesc) handle** can be retrieved by calling ovr_GetHmdDesc(session). The following table describes the fields:

---

| Field | Type | Description |
|:--------|:--------|:--------|
|  Type	|  ovrHmdType	|  Type of the HMD, such as ovr_DK2 or ovr_DK2 .
|  ProductName	|  char[]	|  Name of the product as a string.
|  Manufacturer	|  char[]	|  Name of the manufacturer.
|  VendorId	|  short	|  Vendor ID reported by the headset USB device.
|  ProductId	|  short	|  Product ID reported by the headset USB device.
|  SerialNumber	|  char[]	|  Serial number string reported by the headset USB device.
|  FirmwareMajor	|  short	|  The major version of the sensor firmware.
|  FirmwareMinor	|  short	|  The minor version of the sensor firmware.
|  AvailableHmdCaps	|  unsigned int	|  Capability bits described by ovrHmdCaps which the HMD currently supports.
|  DefaultHmdCaps	|  unsigned int	|  Default capability bits described by ovrHmdCaps for the current HMD.
|  AvailableTrackingCaps	|  unsigned int	|  Capability bits described by ovrTrackingCaps which the HMD currently supports.
|  DefaultTrackingCaps	|  unsigned int	|  Default capability bits described by ovrTrackingCaps for the current HMD.
|  DefaultEyeFov	|  ovrFovPort[]	|  Recommended optical field of view for each eye.
|  MaxEyeFov	|  ovrFovPort[]	|  Maximum optical field of view that can be practically rendered for each eye.
|  Resolution	|  ovrSizei	|  Resolution of the full HMD screen (both eyes) in pixels.
|  DisplayRefreshRate	|  float	|  Nominal refresh rate of the HMD in cycles per second at the time of HMD creation.

---


