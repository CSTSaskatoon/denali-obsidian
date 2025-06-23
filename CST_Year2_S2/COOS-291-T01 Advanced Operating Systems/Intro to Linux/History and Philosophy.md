# History and Philosophy
## Unix History
Written in assembly at Bell Labs (1969) on a PDP-7 microcomputer
Alternative to time-sharing system for a mainframe called Multics
Mostly written by **Ken Thompson** and **Dennis Ritchie**
Moved to PDP-11/20, used for text processing of patent applications

1972, Unix was re-written in C (created by Dennis Ritchie)
- C was considered high level at this point
- since it was written in C, it was relatively portable
- Long time early standard for C was described in the book "The C Programming Language" by Brian Kernighan and Dennis Ritchie

Bell developed multiple versions of Unix and by the early 1980s thousands of people used Unix at AT&T and elsewhere

## Unix Philosophy (Also applies to Linux)
Minimalist, modular software development

Key Principles
- Make programs to do one thing well. To do a new job, build a fresh rather than complicate old programs by adding new features
- Expect the output of every program to become the input of another unknown program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input
- Design and build software, even operating systems to be tried early, ideally within weeks. Don't hesitate to throw away clumsy parts and rebuild them.
- Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tools
- Summary - **Write programs that do one thing and do it well, Write them to work together, and Write programs to handle text streams, because that's a universal interface**

## GNU
**Richard Stallman** - famous for writing Emacs
Started with GNU (Gnu's Not Unix) project to build such an operating system
Re-wrote many of the Unix utilities and use the General Public License (GPL)
- "Free as in speech, not free as in beer"
- Copyleft license

Wrote many utilities, but the GNU Project has one major problem - *they never finished their operating system kernel, the Hurd*

## Minux
Andrew S. Tanenbaum
- Wrote a textbook on Computer Networking
- Wrote an OS textbook and an OS to demonstrate the principles of the textbooks
- OS was called Minux (Mini-Unix) and the source code was widely available, but can only be used for educational purposes

## Linux
Linus Torvalds - student at University of Helsinki
He liked Minux but not the licensing requirements, so he wrote his own kernel
Combined with the tools from the Gnu Project, he was able to put together an OS

### Key Linux websites
[Kernel](https://kernel.org) - Kernel Source Code
[Git](https://git.kernel.org)
[Kernel Newbies](https://kernelnewbies.org) - Learning resource
[Kernel Mailing List](https://lkml.org)
[Linux Weekly News](https://lwn.net)
[Stack Overflow](https://unix.stackexchange.com)

### Difference between Kernel and Operating System Distributions (distros)
Kernel is part of the OS - scheduling tasks, talking to devices, etc.
OS is everything - Kernel, libraries, utilities, etc.
People don't typically build their own Kernel, they use a *distribution* which includes the kernel, utilities, applications, etc.
