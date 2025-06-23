# Make Files
- So far most people have been using Visual Studio to edit, compile and run our programs
- We don't understand what the development environment is doing to complete the process
- In this example, we will manually compile a project into an executable **make file** and the Microsoft compiler **`cl.exe`**

### Process
- `source.c` and `source.h` are compiled to produce object files (`.obj` or `.o` files)
- Object files contain code understandable by the machine
- The linker takes all object files and puts them together in a single executable
- The linker resolves references to functions included in library files (`.a` or `.lib`)
- A `.lib` file is essentially a collection of `.obj` files

### Large Projects
- large software projects can contain many source files
- Each file needs to be compiled
- Some files depend on other files
- To manage the compilling of files, a **makefile** is used.
- The makefile is a text file (called `makefile` with no extension) that lists how files are compiled and linked to the dependencies between files.
- The makefile is executed by a utility called `make` (`nmake` in Microsoft world)
- Before looking at a makefile we need to understand how to compile and link a file on the command line

### Command line compiling and linking
- The C/C++ compiler provided by Microsoft is called **`cl.exe`**
- It's actually an integrated compiler and linker
- For example, suppose you have a source file called `code.c`
- To compile and link the source code, you would do `cl code.c`
- The output would be `code.exe` (or `a.exe` depending on the compiler)

#### Switches
- `-c` - compile only, don't link
- `-o <file>` - places output in a file called `<file>`
- `/Wall` - turn off all warnings
- Case sensitive and vary depending on compiler/linker
- To compile `text.c` to an object file - `cl -c text.c`
- It's important to have system path variable included in the compiler, include files (header files), library files and any other files required by the compiler/linker
- The **Developer Command Prompt For VS 2022** has all these paths set for you automatically, can be launched from the start menu

### Creating a `makefile`
- Consider a statistics project that has some stat functions and contains the following files
	- `mathfuncs.h` - prototypes for all math functions
	- `mathfuncs.c` - implementations of all math functions
	- `display.c` - displays results
	- `stats.c` - man function and test code

#### Dependency Graph
![](Pasted%20image%2020250414103311.png)

- For example, `display.obj` is dependent on the files `display.c` and `mathfuncs.h`
- The file `stats.exe` is dependent on `display.obj`, `mathfuncs.obj` and `stats.obj`
- Each dependency is implemented separately as a target in the make file

### `makefile` syntax
```
target: [dependency list]
	command to execute
```

- Note that a tab before `command` on line 2 **MUST** be used

### Example `makefile`
```
statistics: display.obj mathfuncs.obj stats.obj
	cl display.obj mathfuncs.obj stats.obj
dispay.obj: display.c mathfuncs.h
	cl -c display.c
mathfuncs.obj: mathfuncs.c mathfuncs.h
	cl -c mathfuncs.c
stats.obj: stats.c mathfuncs.h
	cl -c stats.c
```

### Running a `makefile`
- From the directory where the `makefile` exists, run **`nmake`**
- First target will be built
- Notice the order in which the files are built
- Since the target `statistics` is dependent on other targets, the later targets are built first
- The `.obj` files will be visible now if you view the folder where the `makefile` exists
- The executable will be named `display.exe` by default, which can be changed by adding `-o <exe_name>` to the `statistics` target's command (Ex. `cl -o statistics.exe display.obj mathfuncs.obj stats.obj`)

### Rebuilding a project
- Suppose `stats.c` has been modified
- We don't need to recompile the other files, since `nmake` will check the timestamps on the files and only re-create the `.obj` files if the source files have been updated
- Alternatively, the user can run a specified target
- Suppose the file `stats.c` has been changed and needs to be re-compiled for testing
- `nmake` can be called like `nmake stats.obj`

### Other Targets
- Other targets can be added as well
- For example, for administration purposes, a target called *`clean`* or *`remove`* can be added

#### `clean`
```
clean:
	del *.obj *.exe
```

### Constants and Macros
- Represent things that repeat/change
- Ex. what if we switch compilers? - We would need to replace `cl` with something else wherever it occurs
- Instead, we use a macro
- Other variables may need to be changed as well (Ex. `cl.exe` uses `.obj` whereas `gcc` uses `.o` for object files)

#### Example `makefile` with Macros
```
CC=cl
EX=obj
statistics: display.$(EX) mathfuncs.$(EX) stats.$(EX)
	$(CC) display.$(EX) mathfuncs.$(EX) stats.$(EX)
dispay.$(EX): display.c mathfuncs.h
	$(CC) -c display.c
mathfuncs.$(EX): mathfuncs.c mathfuncs.h
	$(CC) -c mathfuncs.c
stats.$(EX): stats.c mathfuncs.h
	$(CC) -c stats.c
clean:
	del *.$(EXE)$ *.exe
```

- Now if we want to switch to using **`gcc`**, we just need to change `CC=gcc` and `EX=o`
