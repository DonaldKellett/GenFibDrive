# GenFibProvider

A simple PSProvider using [SHiPS](https://www.powershellgallery.com/packages/SHiPS/0.8.1) for generating Fibonacci sequences of the nth order, for illustration purposes only

## Supported Platforms

The module has been tested with PowerShell version 5.1.19041.906 on Windows 10 (32-bit) Build 19042.928, though it should work with any sufficiently recent PowerShell version on a sufficiently recent build of Windows 10 on both 32 and 64-bit systems. If you're using PowerShell Core on macOS / Linux (for whatever reason), [YMMV](https://dictionary.cambridge.org/dictionary/english/ymmv).

## Usage

_The following instructions assume Windows 10. If you are using an older version of Windows or a non-Windows operating system, you may need to adapt the instructions accordingly and YMMV._

Note that the default execution policy (see [`about_Execution_Policies`](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.1) for details) on desktop offerings is `Restricted` which will prevent you from using this downloaded module. You may wish to set a more lenient policy such as `RemoteSigned` by invoking the following PowerShell command as administrator:

```powershell
PS> Set-ExecutionPolicy RemoteSigned
```

Please be aware of the potential security implications of running such a command before doing so; I will not be held responsible for any damages to your system that may result.

TODO

## License

[MIT](./LICENSE)
