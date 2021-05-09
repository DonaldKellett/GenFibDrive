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

The module in this repo depends on SHiPS so you will need to install it first (if you haven't done so already) by running the following PowerShell command as administrator:

```powershell
PS> Install-Module -Name SHiPS
```

Answer `Y` for any questions that may come up.

Then, assuming your copy of this repo is located at `C:\path\to\your\GenFibProvider`, run the following PowerShell commands in an existing session or start a new session (administrator rights not required):

```powershell
PS> Import-Module SHiPS
PS> Import-Module C:\path\to\your\GenFibProvider\GenFibProvider.psm1
```

Now you can create a new PSDrive `GF` (or any name to your liking) and navigate to it:

```powershell
PS> New-PSDrive -Name GF -PSProvider SHiPS -Root GenFibProvider#GenFib
PS> Set-Location GF:
```

You should then see the following child items under `GF:\` by running `Get-ChildItem`:

- `Order` (Read-Write): The order of the [generalized Fibonacci sequence](https://en.wikipedia.org/wiki/Generalizations_of_Fibonacci_numbers#Fibonacci_numbers_of_higher_order) as a non-negative integer. Defaults to `2`
- `Start` (Read-Write): The (zero-based) starting index of sequence as a non-negative integer, e.g. for the classic Fibonacci sequence with order 2, we define `F(0) = 0` and `F(1) = 1`. Defaults to `0`
- `Count` (Read-Write): The number of items to return from the sequence, starting from `Start`. Defaults to `10`
- `Sequence` (Read-Only): The generated sequence based on the three items above with type `int[]`, e.g. it is `0, 1, 1, 2, 3, 5, 8, 13, 21, 34` with default parameters

Here, Read means that `Get-Content` is a supported operation and Write means that `Set-Content` is a supported operation.

## Features

- Support for edge cases such as order 0 (where `F(n) = 0` for all `n`) and order 1 (where `F(n) = 1` for all `n`) Fibonacci sequences. Why these definitions make sense is left to the reader as an exercise
- Caching to avoid recomputing the entire sequence if none of the writable items have been written to between invocations of `Get-Content Sequence`

## Possible improvements

- If the writable items are overwritten with the same value, `Get-Content Sequence` will still re-compute the sequence once. Perhaps make it so that overwriting a writable item with the same value is not treated as a modification
- Support more generalizations. Currently, the first `n` terms of an `n`th order Fibonacci sequence is hardcoded with the first `n` terms being `F(k) = 0` (when `k < n - 1`) and `F(n - 1) = 1`. Maybe make it so the first `n` terms can be specified by the user
- 
- ## License

[MIT](./LICENSE)
