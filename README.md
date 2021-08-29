# Overview

SWARMBJECT is a high level programming language and a graphical
development environment for it, including a compiler.

*For newcommers into programming:* computer devices have a
main component, designed to execute instructions called a CPU.
A sequence of instructions is called a code, creating a program.
Such a code can be written in a language that closely resembles
the native instructions of the CPU, called low level programming,
or in a language that can be very different from it, called
high level programming, however this requires translating from
this language to either the native instructions, or to a
different language, to be processed by other programs.
Such a translating program is called a compiler.

# Design goals:

*Portability:*
Instead of directly generating executable code for different
CPU architectures, code shall be generated for different platforms, 
that can be used by specific development tools of that platform.
Note: This is a future goal, as currently only the web platform
is supported, though that still means support for any
device with a web browser available.

*Simplicity:*
Making the base language simple makes learning and porting
it easier.

*Extensive API:*
While the base language is made to be simple, there should be
an extensive set of pre-programmed functionalities (API).
Note: This is a future goal, as currently only what was
needed for the compiler is programmed.

*C/C++ like syntax:*
C and C++ are old but still very popular languages,
with many others based on their syntax. A similar syntax
makes learning the language easier for programmers
already familiar with such languages.

*Asynchronity:*
Modern computers having multiple CPU cores makes it
important to have a programming model that helps
creating applications that can make use of them.

*Distributed:*
Distributed computing means that the application can
not only scale through multiple cores, but even through
multiple computers.
Note: This is a future goal, though this concept is
already in the fundations of the language.

*Web standards:*
The web has many well standardized and known technologies,
designed to work through a wide variety of devices.

*Documentation:*
Documentation shall be provided for every user facing 
feature of the language and its API in a simple and
understandable way, and also with such an example.
Note: This is a future goal, as currently only a
tutorial is presented.

# Architecture

A SWARMBJECT application consists of a hierarchy of instances,
that can be distributed through multiple computers.
Note: This is a future goal, as currently 
only one instance is supported.
Each instance can contain multiple threads of execution.
During its run, the application can create asynchronous 
(independent) objects, each assigned to a thread.
An async object can contain data, that other async objects
can not access, and it can communicate with other
async objects by calling their named async functionalities.
Note: The way that async objects can only 
access their own data, but not others, was a
design choice, since these objects might not be
in the same computer, making such access inefficient,
furthermore due to asynchronity, multiple async 
objects might try to access the same data at the
same time, called a data race, that can result in 
unexpected behaviour. Instead by calling async 
functions, the callee does not have to wait for the call
to run, as that will be executed independently,
and each thread can execute only one async function
at the same time, while any others in the same thread
has to wait, making data races not possible.

# Tutorial

Lets create an application that models a situation, where
a manager gives a calculating task to a scientist, and
expects the result back when it is done, and instructs
a marketeer to display it to us, the Boss.

Download SWARMBJECT.html, SWARMBJECT.js and std.saf from the
releases to a folder on your device, and open the html.
To access the menu, tap or click the top colored header bar.
Create a folder for the tutorial with "Browse", "/",
"New folder", name it "tut", and choose "Create".
In the same way create a folder named "src" ("/tut/",
"New folder", Name: "src", "Create"). Upload the 
downloaded std file to it ("/tut/src/", "Upload" the file). 
Now create a file named "Main.scf"
("/tut/src/", "New file", Name: "Main.scf",
"Create"). Tap or click on "Main.scf",
and choose "Select", to open the file for editing.
Tap or click in the empty bordered area below
the top bar and type in the code:

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		Manager aptr manager = new(app, 0) Manager;
		manager.start(app);
	}
}
```

The code of a SWARMBJECT application has a well defined
structure. It has to be in SWARMBJECT class files (".scf"),
in a folder named "src". Each file defines a class,
that objects can be created from. When the application
starts, it automatically creates an
"std::ApplicationInstance" async object. When a class 
file is not directly in the src folder, but in a
sub folder, then the "::" token is used. Thus the
"ApplicationInstance.scf" file is in the "std" folder,
but the programming term for it is that the
"ApplicationInstance" class is in the "std" namespace.
The "std" namespace contains the standard pre-programmed 
functionalities of the language, thus it is the API.
Async objects can contain non-async objects as their
data, so other async objects can not access these.
The "std::ApplicationInstance" async object 
contains a non-async "Main" object. This was a
design choice to be able to extend the
"std::ApplicationInstance" class with custom
data through the "Main" class, since many
functionalities are only available through the
"std::ApplicationInstance" class. The "Main" object
has to have a "main" function, that is called by the
"std::ApplicationInstance" object at the application
start, with also passing a reference to itself named as
the "app" parameter. The "aexcl" specifier indicates
that it is possible to access its members (data and
functions), since "main" is a function of the
"Main" object, that is part of the
"std::ApplicationInstance" object. The "main"
function creates a new "Manager" async object, and
a reference to it is stored in the "manager" variable.
The "aptr" specifier indicates, that it is not
possible to access its data from the "main" function,
as it is another async object, thus not part of the
"std::ApplicationInstance" async object, since
while async objects can contain non-async objects,
but can not contain other async objects, only
references to them. Thus async objects are always
independent. The parameters of the "new" operator
specified that the new "Manager" async object
is assigned to thread 0 (this is the first thread,
as indexing starts with 0) of the same instance as the
"app" object. In order for the "Manager" async 
object to start doing its job, its "start" async 
function is called, with the reference to the
"app" object, as the manager will need it later,
to display the result.

Open again the menu, and choose "Save opened file".
Now create "Manager.scf" in "src", the same 
way as "Main.scf", with the code:

```
async class Manager {

	std::ApplicationInstance aptr instance;
	
	async void start(
		std::ApplicationInstance aptr app){
		instance = app;
		Scientist aptr scientist = new(app, 1) Scientist;
		scientist.calculate(this);
	}
	
	async void calculated(
		unsigned int result){
		Marketeer aptr marketeer =
			new(instance, 1) Marketeer;
		marketeer.display(result, instance);
	}
}
```

The "start" function is async, as async objects 
can only communicate with async functions, while 
non-async functions, like the "main" function 
can only be used in the same async object. The 
"start" async function stores the "app" reference
in the "instance" data member of the "Manager" async 
object. A new "Scientist" async object is created 
in thread 1, and stored in the "scientist" variable.
The "app" parameter, the "instance" data member
and the "scientist" variable is "aptr", since 
the "Manager" object can only reference, but
not access their data. The scientist is instructed 
to calculate, by calling its async function with
a reference to the manager, as the "this" keyword 
always points to the associated object of the 
current function. The "calculated" async 
function will be called by the scientist with the
result, that is a positive (unsigned) integer, to be
sent to a marketeer in thread 1, in order to display 
it in the instance.

Create "Scientist.scf" in "src", with the code:

```
async class Scientist {

	async void calculate(
		Manager aptr manager){
		unsigned int result;
		/*After a long and complicated calculation.*/
		result = 2021;
		manager.calculated(result);
	}

}
```

The scientist calculates the result, and calls the 
"calculated" async function of the manager.

Saving the file, and create "Marketeer.scf"
in "src", with the code:

```
async class Marketeer {

	async void display(
		unsigned int result,
		std::ApplicationInstance aptr app){
		onScreen(result, app);
	}

	static async void onScreen(
		unsigned int result,
		std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node body;
		std::html::Document::getBody(&document, &body);
		std::DString string;
		string.addUint(result,
			std::NumberBases::decimal);
		std::dom::Node text;
		std::dom::Text::create(&document, &text,
			string.data, 0, string.length);
		body.appendChild(&text);
	}

}
```

The marketeer decided that the result is most impactful,
if it is displayed on the screen. However to do that, 
accessing "std::ApplicationInstance" data that 
"Marketeer" can't is needed. Adding an async function 
to "std::ApplicationInstance" would be needed, 
however that file should not be edited, since it is
part of the API. To solve this, a static async function 
can be used. Functions declared as static don't have
an associated object, thus they can access only the 
function parameters, while non-static functions can also 
access the associated object's data. This is how
the "calculated" function can access the "instance" 
data member of the manager, since it is a non-static 
function having the manager object associated with it.
A static async function by not having an associated 
object, can have an "aexcl" parameter instead, making
the function to run on that parameter's thread, 
and accessing its data. Thus the "onScreen" function 
can access the "app" data. This function uses the
BOM, DOM and HTML web standard, describing the structure 
of documents as a hierarchy of nodes, that a web 
browser displays. The objects and functions used in 
"onScreen" are non-async, for performance reasons.
The "getWindow" function sets the referenced 
"window" object, to point to the graphical window 
of the instance. The "&" addressof operator is used
to give the function a reference to the non-async 
"window" object. The "document" object is set to 
point to document that the window displays. The
content of the document is in its body node,
and the "body" object is set to point to it. 
The "result" is a number, that has to be converted 
to a string (textual data). A text node is created
from the string, containing the full length of its 
data, and it is appended to the body of the document,
for the browser to display it.

Save the file, and in the menu, choose "Compile",
"/", "..", "/tut/", "Select". Use "Compile" under
the selected path, and wait until it finishes. Set
the number of threads to use from the default 
1 to 2, with "Cancel", "Browse", "html/",
"compiled.html", and almost at the bottom 
change "_run(1)" to "_run(2)". Save the file in 
the menu and choose "Compile" and "Run" at the 
bottom. This requires a popup, and the 
browser might ask you to allow it.

# Backups

Creating a backup as a safety measure is done with
"Browse" in the menu, navigate to a folder, choose
its path, and "Download". Now if the folder is
deleted, like by choosing its path, and "Delete",
it can be uploaded back by choosing a folder path
and "Upload" the backup file.

# Contribute

In order to contribute, you have to certify that:

```
Developer Certificate of Origin
Version 1.1

Copyright (C) 2004, 2006 The Linux Foundation and its contributors.

Everyone is permitted to copy and distribute verbatim copies of this
license document, but changing it is not allowed.


Developer's Certificate of Origin 1.1

By making a contribution to this project, I certify that:

(a) The contribution was created in whole or in part by me and I
    have the right to submit it under the open source license
    indicated in the file; or

(b) The contribution is based upon previous work that, to the best
    of my knowledge, is covered under an appropriate open source
    license and I have the right under that license to submit that
    work with modifications, whether created in whole or in part
    by me, under the same open source license (unless I am
    permitted to submit under a different license), as indicated
    in the file; or

(c) The contribution was provided directly to me by some other
    person who certified (a), (b) or (c) and I have not modified
    it.

(d) I understand and agree that this project and the contribution
    are public and that a record of the contribution (including all
    personal information I submit with it, including my sign-off) is
    maintained indefinitely and may be redistributed consistent with
    this project or the open source license(s) involved.
```

by including a 
```
Signed-off-by: your name <your e-mail>
```
line in the commit message.

It is highly recommended that you describe a plan
of your contribution, by creating an issue,
before coding it, to save you the time in case it
does not align well with the current SWARMBJECT goals,
or if modifications are needed.

By creating an issue, you agree, that the ideas described
in the issue may be implemented under the license
of the SWARMBJECT project.

# Software license

Copyright (c) 2021 SWARMBJECT contributors

Redistribution and use in source and binary forms,
with or without modification, are permitted
provided that the following conditions are met:

1. Redistributions of source code must
retain the above copyright notice, this list
of conditions and the following disclaimer.

2. Redistributions in binary form must
reproduce the above copyright notice,
this list of conditions and the following 
disclaimer in the documentation and/or other 
materials provided with the distribution.

Subject to the terms and conditions of this
license, each copyright holder and contributor
hereby grants to those receiving rights under this
license a perpetual, worldwide, non-exclusive,
no-charge, royalty-free, irrevocable (except for
failure to satisfy the conditions of this license)
patent license to make, have made, use, offer to
sell, sell, import, and otherwise transfer this
software, where such license applies only to
those patent claims, already acquired or hereafter
acquired, licensable by such copyright holder or
contributor that are necessarily infringed by:

(a) their Contribution(s) (the licensed
copyrights of copyright holders and
non-copyrightable additions of contributors,
in source or binary form) alone; or

(b) combination of their Contribution(s)
with the work of authorship to which such
Contribution(s) was added by such copyright
holder or contributor, if, at the time the
Contribution is added, such addition causes
such combination to be necessarily infringed.
The patent license shall not apply to any other
combinations which include the Contribution.

Except as expressly stated above, no rights or
licenses from any copyright holder or contributor
is granted under this license, whether expressly,
by implication, estoppel or otherwise.

DISCLAIMER

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS
AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
SUCH DAMAGE.

# Documentation license

Copyright (c) 2021 SWARMBJECT contributors

Redistribution and use in source and binary forms,
with or without modification, are permitted
provided that the following conditions are met:

1. Redistributions in source form must
retain the above copyright notice, this list
of conditions and the following disclaimer.

2. Redistributions in binary form must
reproduce the above copyright notice,
this list of conditions and the following 
disclaimer in the documentation and/or other 
materials provided with the distribution.

Subject to the terms and conditions of this
license, each copyright holder and contributor
hereby grants to those receiving rights under this
license a perpetual, worldwide, non-exclusive,
no-charge, royalty-free, irrevocable (except for
failure to satisfy the conditions of this license)
patent license to make, have made, use, offer to
sell, sell, import, and otherwise transfer this
documentation, where such license applies only to
those patent claims, already acquired or hereafter
acquired, licensable by such copyright holder or
contributor that are necessarily infringed by:

(a) their Contribution(s) (the licensed
copyrights of copyright holders and
non-copyrightable additions of contributors,
in source or binary form) alone; or

(b) combination of their Contribution(s)
with the work of authorship to which such
Contribution(s) was added by such copyright
holder or contributor, if, at the time the
Contribution is added, such addition causes
such combination to be necessarily infringed.
The patent license shall not apply to any other
combinations which include the Contribution.

Except as expressly stated above, no rights or
licenses from any copyright holder or contributor
is granted under this license, whether expressly,
by implication, estoppel or otherwise.

DISCLAIMER

THIS DOCUMENTATION IS PROVIDED BY THE COPYRIGHT HOLDERS
AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS
DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY OF
SUCH DAMAGE.