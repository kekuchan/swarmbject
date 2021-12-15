# "std::fs::FileSystem" class:

Used for file system operations.
	
## "gui" data member:

Used to show a graphical user interface. Its 
members will be detailed at "std::fs::GUI".

## "deleteFile" member function:

Requests to delete a file.

Parameters:
* The file's path as a 0 ended 
unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, std::str::String*)" function 
that will be called later asynchronously after the 
deletion, with the instance and the file's path.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.deleteFile(
			"/tut/Year.md", onDeleted);
	}
	
	static void onDeleted(
		std::ApplicationInstance aexcl app,
		std::str::String* path){
	}
}
```

## "deleteFolder" member function:

Requests to delete a folder.

Parameters:
* The folder's path as a 0 ended 
unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, std::str::String*)" function 
that will be called later asynchronously after the 
deletion, with the instance and the folder's path.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.deleteFolder(
			"/tut/", onDeleted);
	}
	
	static void onDeleted(
		std::ApplicationInstance aexcl app,
		std::str::String* path){
	}
}
```

## "openFile" member function:

Requests to open a file.

Parameters:
* The file's path as a 0 ended 
unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, std::fs::File*)"
function that will be called later 
asynchronously after the open, with the 
instance and a pointer to the file.
* The file's open mode as an 
std::fs::OpenFileModes value.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.openFile(
			"/tut/Year.md", onOpened,
			std::fs::OpenFileModes::readBinary);
	}
	
	static void onOpened(
		std::ApplicationInstance aexcl app,
		std::fs::File* file){
	}
}
```
		
## "openFolder" member function:

Requests to open a folder.

Parameters:
* The folder's path as a 0 ended 
unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, std::fs::Folder*)"
function that will be called later asynchronously 
after the open, with the instance and a pointer 
to the folder.
* A boolean value whether to create 
the folder if it does not exists.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.openFolder(
			"/tut/", onOpened, true);
	}
	
	static void onOpened(
		std::ApplicationInstance aexcl app,
		std::fs::Folder* folder){
	}
}
```

## "moveFile" member function:

Requests to move with possibly renaming a file.

Parameters:
* The file's path to move from as a 
0 ended unsigned char array string.
* The file's path to move to as a 
0 ended unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, unsigned char[],
unsigned int)" function	that will be called later 
asynchronously after the move, with the instance, 
the file's path as a 0 ended unsigned char array 
string, and the path's starting offset in the array.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.moveFile("/tut/Year.md",
			"/tutorial/Year.md", onMove);
	}
	
	static void onMove(
		std::ApplicationInstance aexcl app,
		unsigned char[] path, unsigned int offset){
	}
}
```

## "moveFolder" member function:

Requests to move with possibly renaming a folder.

Parameters:
* The folder's path to move from as a 
0 ended unsigned char array string.
* The folder's path to move to as a 
0 ended unsigned char array string.
* Either nullptr, or a pointer to a "void(
std::ApplicationInstance, unsigned char[],
unsigned int)" function	that will be called later 
asynchronously after the move, with the instance, 
the folder's path as a 0 ended unsigned char array 
string, and the path's starting offset in the array.

Returns: 0, if no immediate error, >0 otherwise.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		app.fileSystem.moveFolder("/tut/",
			"/tutorial/", onMove);
	}
	
	static void onMove(
		std::ApplicationInstance aexcl app,
		unsigned char[] path, unsigned int offset){
	}
}
```

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