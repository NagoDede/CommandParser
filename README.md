# CommandParser
Command Parser is a windows command line parser (never tested under linux, but could run).
It was build on a code found on https://www.codeproject.com/Articles/42113/CommandParser-A-getopt-Inspired-Command-Line-Parse

I did some modifications to catch more specifically my needs, but the original code remains the same.

I personnaly use this as a dll in my .Net projects (C# and VB.net) without troubles. With the appropriate COM interfaces, it should run smoothly with C++ or other langage.


## Usage 
It is quite simple and personnaly, I create a specific class or module to initiate the options managed by the parser. 
For software with several and complexes options, the dedicated class will manage in details the interface and flags (i.e. Check that the reaiured file exists...). 
If the usage is simple, I create a private structure which will reflect the arguments and options set, and the InitParse function is used to initialise the parser.
you can't directly return the structure from the function, else it return a non initialized structure (which is not the expected result). This is why I use a private structure and set the InitParse function in my main module / classe.
Basic code is:
```vb
parseOptions As parserOptions
    Dim parser As New CommandParser
    InitParse(parser)
    parser.Parse()
 ```
        
The definition of the arguments and options remains identical to the original code (refer to https://www.codeproject.com/Articles/42113/CommandParser-A-getopt-Inspired-Command-Line-Parse).

For a very simple case, my InitParse function is
```vb
Private Sub InitParse(ByRef parser As CommandParser)
        parseOptions.InputDir = WIN_DIR_INSTALLER
        parseOptions.MoveDir = DFLT_DIR_MOVE
        parseOptions.ReportPath = DFLT_PATH_REPORT
        parseOptions.toDelete = False
        parseOptions.toMove = False
        parseOptions.toShowHelp = False
        parseOptions.toReport = False
        parseOptions.toSimulate = False


        parser.Argument("d", "delete", "delete the relevant files", "delete",
                CommandArgumentFlags.HideInUsage,
                Sub(p, v)
                    parseOptions.toDelete = True
                    parseOptions.toMove = False
                End Sub
                )

        parser.Argument("m", "move", "Move the relevant files to the specificed directory - default: " &
                        parseOptions.MoveDir, "inputFile",
                CommandArgumentFlags.TakesParameter,
               Sub(p, v)
                   parseOptions.toDelete = False
                   parseOptions.toMove = True
                   If Not String.IsNullOrEmpty(v) Then
                       parseOptions.MoveDir = v
                   End If
               End Sub)

        parser.Argument("s", "simulate", "Simulate the action and write the report in the indicated file [" &
                        parseOptions.ReportPath & "]",
                        "simulate",
                CommandArgumentFlags.TakesParameter,
                 Sub(p, v)
                     parseOptions.toSimulate = True
                     parseOptions.toReport = True
                     If Not String.IsNullOrEmpty(v) Then
                         parseOptions.ReportPath = v
                     End If

                 End Sub)

        parser.Argument("h", "help", "Display this help message", "help",
                CommandArgumentFlags.HideInUsage,
             Sub(p, v)
                 parseOptions.toShowHelp = True
             End Sub)

        parser.Argument("r", "report", "Write the report at the indicated path [" & parseOptions.ReportPath & "]", "report",
                CommandArgumentFlags.TakesParameter,
                Sub(p, v)
                    parseOptions.toReport = True
                    If Not String.IsNullOrEmpty(v) Then
                        parseOptions.ReportPath = v
                    End If

                End Sub)
    End Sub
 ```
 
 ## Other
 In the same way, ndesk.org propose an other command line parser.
 refer to http://ndesk.org/Options
        
        



