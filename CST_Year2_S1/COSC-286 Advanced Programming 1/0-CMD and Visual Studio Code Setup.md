We are using *Visual Studio Code* for our C# file management.
Install C#, C# Dev Kit, .Net Core Test Explorer, as well as Test Adapter Converter and Test Explore UI.
### Starting a file with CMD
Open CMD.
Create a source directory to run executables since the school now only allows like three places where executables can be ran from.
`cd c:\` to navigate to c drive.
`mkdir sourcecode` to make the directory that can run all executables, it must be this name exactly.
Here we can make our other subdirectories. Use the `cd` command to go to the new directory and `mkdir` to create more directories.
Example: `cd .\sourcecode`, `cd sourcecode` or more directly `cd c:\sourcecode`.

Once you are at the directory you want to make your projects enter the following command:
`dotnet new console -o ./ProjectName`

You can edit the file from Visual Studio Code from here.
### Visual Studio Code
On the Tool bar at the top open the *Terminal*.

Using the cmd (terminal in the app) use `cd ProjectName` to find your project.
Use `dotnet build` to build a project and use `dotnet run` to run it. You do not need to build before you run, can you just simple compile each time you run it.

>Be sure to save a file manually each time you change it and BEFORE you build it.
### Linking Classes together - like imports
Make another class with the same root directory.
`dotnet new console -o ./MyClasses`. I'd like to add that this may be incorrect, pretty sure it'll work.
Make the class with some methods like Java.
Build the class with `dotnet build` and you do NOT need to run it (it also does not have a main typically).

In the class with the main, add `using MyClasses` to the top like a Java import.
Navigate to the main class with the terminal and input this command:
`dotnet add reference ..\MyClasses\MyClasses.csproj`

You can now run any method that came from that reference class.