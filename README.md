# CommandParser
Command Parser is a windows command line parser (never tested under linux, but could run).
It was build on a code found on https://www.codeproject.com/Articles/42113/CommandParser-A-getopt-Inspired-Command-Line-Parse

I did some modifications to catch more specifically my needs, but the original code remains the same.

I personnaly use this as a dll in my .Net projects (C# and VB.net) without troubles. With the appropriate COM interfaces, it should run smoothly with C++ or VB langage.


##Usage 
It is quite simple and personnaly, I create a specific class or module to initiate the options managed by the parser. 
For software with several and complexes options, the dedicated class will manage in details the interface and flags (i.e. Check that the reaiured file exists...). If the usage is simple, I create a structure which will reflect the arguments and options set. 

Basic code is:
        Dim parser As New CommandParser
        InitParse(parser)
        parser.Parse()
        
 while the definition remains identical to the original code (refer to https://www.codeproject.com/Articles/42113/CommandParser-A-getopt-Inspired-Command-Line-Parse).
 
 ##Other
 In the same way, ndesk.orh propose an other command line parser.
 refer to http://ndesk.org/Options
        
        



