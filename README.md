### Minidumper

Minidumper is a command-line tool that can capture dump files of .NET processes in three modes: **minimal**, which is enough just for basic triage; **heap**, which includes managed heap information and other data required to diagnose more intricate .NET issues; and **full**, which creates a complete dump file.

What makes Minidumper interesting is the **heap** mode. For large applications, especially with a lot of modules or when unmanaged memory and code are involved, dumps generated by the **heap** mode can be 5x or 10x smaller than full memory dumps, but will still allow complete investigation of many .NET issues by tools like Visual Studio and WinDbg (SOS).

### DumpWriter

Also included is a stand-alone library (DumpWriter) that can be added to any project to capture dumps of arbitrary processes. The DumpWriter project also contains the full interop signatures for the Win32 `MiniDumpWriteDump` API and all associated data structures, including callback input and output structures.

> #### NOTES
> * To create dumps of 32-bit processes, make sure to use the 32-bit version of the application -- and vice versa for 64-bit.
> * .NET 4.6 is currently not supported because of a limitation in CLRMD. You can work around this in the meantime by compiling your own version of CLRMD from [this pull request](https://github.com/Microsoft/dotnetsamples/pull/23/files).
> * MiniDumper has gone through very minimal testing. Although it is unlikely that it will cause any damage to the target process (if dump generation fails, MiniDumper exits and the target continues running), but YMMV.

### Usage

```
  --pid        The id of the process to dump.

  --pn         The name of the process to dump.

  -f           Required. The name of the dump file to create.

  --mini       Create a minimal dump file, enough to diagnose crashes and
               display call stacks.

  --heap       Create a dump file with the CLR heap, but without module code or
               unmanaged memory contents.

  --full       Create a complete dump file with the full memory address space.

  -v           Get detailed diagnostic output from the dump capturing process.

  --help       Display this help screen.

  --version    Display version information.
```
