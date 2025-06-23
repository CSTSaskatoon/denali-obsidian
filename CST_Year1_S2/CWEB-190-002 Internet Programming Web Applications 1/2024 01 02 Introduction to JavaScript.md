---
quickshare-date: 2024-01-10 11:24:24
quickshare-url: "https://noteshare.space/note/clr81vusm174201mwwmlhkcq2#/NvB84i1lQV/QK45+bZuDEb0CAc+erTHA7apiPV1pJI"
---
Objectives
	What is Javascript and how does it work?
	Basic Javascript programming
	other stuff
	
---
# NOTES

### What is JavaScript
	HTML Pages - Content
	CSS - Style
	JavaScript - Behaviour
	Interpreted Language
		Java, C++ and other languages. JavaScript is not compiled but interpreted which means it's executed by a runtime environment. In our case, as it's code is encoured within thebrowser
		One implication of this is regarding errors. A JavaScript program can contain errors and still execute. It will execute until an error is encountered
		Interpreted languages are generally slower but since JavaScript is used for fairly simple functions it's not a problem
	JavaScript (in our case) is executed by the browser
		Web pages and JavaScript are recieved from a web server but the scripts are executed by the web browser on your computer
		The web browser is the run-time environment for JavaScript
		Server-side JavaScript is possible
	All Modern Browsers support JavaScript
		Some users may disable JavaScript
		Some organizations may mandate older browser versions for compatability reasons
		Not all browsers support JavaScript in the exact same way (This has gotten better)
		Implications of this is the need to
			Test your JavaScript on multiple browsers on multiple platforms
			Design your dynamic pages with graceful degredation in case JavaScript is turned of or unavailable
### Review
	Client requests web page from a web server, server provides web page data
	Keywords
		HTTP - Hyper Text Transfer Protocol
		GET
		POST
	Step 1 - files recieved (html,htm,xhtml,css,js,jpg,gif,etc)
	Step 2 - Browser processes html file to tell how to display the page
		Identify the css, scripting, images and other seperate files
	Step 3 - Process External files as tehy are encountered or specified
	Validation is done on both
### JavaScript Applications
	JavaScript can be used for
		Dynamic HTML - generate or modify HTML interactively
		User Interaction - dialog boxes or other user input
		Form Validation - use alongside HTML forms
		AJAX (Asyncronous JavaScript and XML) - contact another server and retrieve information in XML or JSON format
	JavaScript can't
		Access the local file system
		Make arbitrary network connections (Sandboxed within the environment)
### Java vs JavaScript
	These two languages are not related
	They do have similar syntax because they were both designed with C-like syntax
	Both have objects, but they work differently
	Most operators and control structures work the same or similar
	Differences
		Java is compiled and interpreted, JavaScript is interpreted
		A java program is compiled to bytecode as a .class file which is then executed within a Java VM
		JavaScript code is executed directly by the run-time environment (browser)
		Different Typing
			Java is a strongly, statically typed - types checked at compile time and never change (int cannot be changed to a String)
			JavaScript is loosely, dynamically typed - types checked at run time and can change, but doesn't mean you should (int can be changed to a String)
	