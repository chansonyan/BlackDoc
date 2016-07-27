---
layout: post
title: 【Debug】LINK2019 Unresolved External Symbol
categories: Visual_Studio_Debug
tags: Debug Visual_Studio
---



-------------------
## **Problem1:** 
Create a new project in Visual Studio 2015 while Exploring Oculus PC SDK Demos,(File->New->Project->Visual C++->Win32->Win32 Project(**I should choose Win32 Console Project here**)->OK->Select Empty->Finish)

Then I Create a new main.cpp file whih code:
```C++
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

	ovrHmdDesc desc = ovr_GetHmdDesc(session);
	ovrSizei resolution = desc.Resolution;

	ovr_Destroy(session);
	ovr_Shutdown();
}


//
int main()
{

	Application();
	return(0);
}
```

Build Solution, and I got the following errors:

> error LINK2019: unresolved external symbol _WinMain@16 referenced in function ___tmainCRTStartup

---
**[Solution:](http://stackoverflow.com/questions/6626397/error-lnk2019-unresolved-external-symbol-winmain16-referenced-in-function)**

> Thats a linker problem.
> 
> Try to change **Properties -> Linker -> System -> SubSystem** (in Visual Studio).
> 
> from Windows (/SUBSYSTEM:WINDOWS) to Console (/SUBSYSTEM:CONSOLE)






---
# Problem2:
在一个Solution中包含了其他Projects，Projects之间有Dependency关系，通过Solution Explorer中右键工程->Build Dependencies->Project Dependencies设置好后，Build遇到LINK2019，

Solutions：
https://msdn.microsoft.com/en-us/library/799kze2z.aspx
第八条指的就是这个问题：
- A build dependency is only defined as a project dependency in the solution. In earlier versions of Visual Studio, this level of dependency was sufficient. However, starting with Visual Studio 2010, Visual Studio requires [a project-to-project reference](https://msdn.microsoft.com/en-us/library/ez524kew.aspx). If your project does not have a project-to-project reference, you may receive this linker error. Add a project-to-project reference to fix it.

也就是Projects之间还需要添加下Reference关系。

---

