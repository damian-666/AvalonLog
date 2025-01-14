# AvalonLog

![code size](https://img.shields.io/github/languages/code-size/goswinr/AvalonLog.svg) 
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

![logo](https://raw.githubusercontent.com/goswinr/AvalonLog/main/Doc/logo400.png)

AvalonLog is a fast and thread-safe WPF text log viewer for colored text. Including F# printf formatting . Based on [AvalonEditB](https://github.com/goswinr/AvalonEditB). Works on .NET Framework 4.7.2 and .NET 6.0

Thread-safe means that it can be called from any thread.

Fast means 
- it buffers repeated print calls and updates the view maximum 10 times per second. see ![source](https://github.com/goswinr/AvalonLog/blob/main/Src/AvalonLog.fs#L222)
- Avalonedit is fast, the view is virtualized. It can easily handle thousands of lines.  

### Usage

Here an short example for F# interactive in .NET Framework.
(for net6.0 you would have to use it in a project)

```fsharp
#r "PresentationCore"
#r "PresentationFramework"
#r "WindowsBase"

#r "nuget: AvalonLog"

open System.Windows

let log = new AvalonLog.AvalonLog() // The main class wrapping an Avalonedit TextEditor as append only log.

// create some printing functions by partial application:
let red   = log.printfColor 255 0 0  // without newline
let blue  = log.printfnColor 0 0 255 // with newline
let green = log.printfnColor 0 155 0 // with newline

// print to log using F# printf formatting
red   "Hello, "
blue  "World!"
red   "The answer"
green " is %d." (40 + 2)

Application().Run(Window(Content=log))  // show WPF window 
```
this will produce 

![WPF window](https://raw.githubusercontent.com/goswinr/AvalonLog/main/Doc/HelloWorld.png)


For C# there is  
```csharp
public void AppendWithBrush(SolidColorBrush br, string s)
```
and similar functions on the `AvalonLog` instance.
### Documentation

See extracted API at [fuget.org](https://www.fuget.org/packages/AvalonLog/0.7.2/lib/net472/AvalonLog.dll/AvalonLog)  

### License

MIT

Logo by [LovePik](https://lovepik.com/image-401268798/crystal-parrot-side-cartoon.html)

### Changelog 

`0.7.3`
- update readme, fix typos

`0.7.2`
- fix typos in readme

`0.7.1`
- use AvalonEditB `1.4.1`
- fix typos in docstrings

`0.7.0`
- fix crash when Log has more than 1000k characters

`0.6.0`
- fix ConditionalTextWriter

`0.5.0`
- Update to AvalonEditB `1.3.0`
- target net6.0 and net472
- fix typos in docstring

`0.4.0`
- Update to AvalonEditB `1.2.0` 
- Rename `GetTextWriterIf` to `GetConditionalTextWriter`

 `0.3.1` 
- Update Xml Docstrings