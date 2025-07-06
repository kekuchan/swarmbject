# "std::fs::Entry" class:

Used to point to a file system entry.

```
class Main {
	
	std::fs::Entry file;
	std::ds::BufferView parameters;
	std::str::String string;
	
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		file.set("tmp://tut/Year.md", 0, 17, 
			std::fs::FileModes::read,
			onOpened, 0, &parameters);
		file.open(app);
	}
	
	static void onOpened(
		std::ApplicationInstance aexcl app,
		std::fs::Entry* file,
		unsigned int error){
		app.main.parameters.data = 
			app.main.string.create(4);
		app.main.parameters.size = 4;
		file->callback = onReadOrWrite;
		file->read(app);
	}
	
	static void onReadOrWrite(
		std::ApplicationInstance aexcl app,
		std::fs::Entry* file,
		unsigned int error){
		file->callback = onClosed;
		file->close(app);
	}
	
	static void onClosed(
		std::ApplicationInstance aexcl app,
		std::fs::Entry* file,
		unsigned int error){
	}
	
}
```

## "callback" data member:

Either nullptr, or a pointer to a "void(
std::ApplicationInstance, std::fs::Entry*,
unsigned int)" function that will be called 
after the requested operation was completed.

```
/*In Main::main, instead of the set*/
file.callback = onOpened;
```

## "cursor" data member:

The cursor's position as an unsigned int.

```
/*In Main::main, instead of the set*/
file.cursor = std::val::Uint::maximum;

/*In Main::onOpened.*/
unsigned int cursor = file->cursor;
/*The file's size.*/
```

## "mode" data member:

The entry's mode of operation as an 
std::fs::FileModes or std::fs::FolderModes 
value. It should not be modified while open.

```
/*In Main::main, instead of the set*/
file.mode = std::fs::FileModes::read;
```

## "parameters" data member:

Some parameters to be used by the 
requested operation as a void*.

```
/*In Main::main, instead of the set*/
file.parameters = &parameters;
```

## "path" data member:

The entry's path as std::str::DString.
It should not be modified while open.

```
/*In Main::main, instead of the set*/
file.path.setCString("tmp://tut/Year.md");
```

## "state" data member:

The entry's current state as an 
std::fs::EntryStates, std::fs::FileStates or 
std::fs::FolderStates value. 

```
/*In Main::onOpened.*/
unsigned char state = file->state;
/*std::fs::FileStates::open*/
```

## "close" member function:

Requests to close the open entry.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
/*In Main::onOpened.*/
file->callback = onClosed;
file->close(app);
```

## "info" member function:

Copies some info about the entry 
to an unsigned char array.

Parameters:
* The type of info 
as an std::fs::InfoModes value. 
* The unsigned char array to copy to.
* The starting index of the array to copy to.

Returns: the length of the character data.

```
class Main {
	std::fs::Entry folder;
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		folder.set("tmp://tut/", 0, 10, 
			std::fs::FolderModes::each,
			onOpened, 0, nullptr);
		folder.open(app);
	}
	static void onOpened(
		std::ApplicationInstance aexcl app, 
		std::fs::Entry* folder, 
		unsigned int error){
		if (folder->state == 
			std::fs::FolderStates::none){
			/*Iterated over all the entries.*/
			return;
		}
		unsigned int length = folder->info(
			std::fs::InfoModes::name, nullptr, 0);
		std::str::DString string;
		folder->info(std::fs::InfoModes::name, 
			string.create(length), 0);
		/*"Year.md"*/
	}
}
```

## "infoDString" member function:

Inserts some info about the entry 
to an std::str::DString's end.

Parameters:
* The type of info 
as an std::fs::InfoModes value. 
* A pointer an std::str::DString.

Returns: void.

```
class Main {
	std::fs::Entry folder;
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		folder.set("tmp://tut/", 0, 10, 
			std::fs::FolderModes::each,
			onOpened, 0, nullptr);
		folder.open(app);
	}
	static void onOpened(
		std::ApplicationInstance aexcl app, 
		std::fs::Entry* folder, 
		unsigned int error){
		if (folder->state == 
			std::fs::FolderStates::none){
			/*No more entries.*/
			return;
		}
		std::str::DString string;
		file->infoDString(
			std::fs::InfoModes::name, &string);
		/*"Year.md"*/
	}
}
```

## "open" member function:

Requests to open a file.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
/*In Main::main.*/
file.open(app);
```

## "read" member function:

Requests to read to an std::ds::BufferView 
a sequence of unsigned char values from the file 
starting at the cursor's position, and increases 
the cursor with the number of values read.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
/*In Main::onOpened.*/
app.main.parameters.data = 
	app.main.string.create(4);
app.main.parameters.size = 4;
file->callback = onReadOrWrite;
file->read(app);

/*In Main::onReadOrWrite.*/
std::str::String* string = &app.main.string;
/*"2025"*/
```

## "readCall" member function:

Requests to read to an std::fs::Call 
a sequence of unsigned char values from the file 
starting at the cursor's position, and increases 
the cursor with the number of values read.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
class ReadCall : std::fs::Call {
	std::ds::DBuffer buffer;
	ReadCall(){
		call = (void())set;
	}
	static void set(
		std::fs::Call* call, 
		unsigned int cursor, 
		unsigned char value){
		(ReadCall*)call->buffer.addU8(value);
	}
}

/*Change "std::ds::BufferView" 
	to "ReadCall" in Main.*/

/*Change Main::onOpened.*/
app.main.parameters.size = 
	std::val::Uint::maximum;
file->callback = onReadOrWrite;
file->readCall(app);

/*In Main::onReadOrWrite.*/
std::ds::DBuffer* buffer = 
	&app.main.parameters.buffer; /*'2','0','2','5'*/
unsigned int size = 
	app.main.parameters.size; /*4*/
```

## "set" member function:

Sets the entry's data members.

Parameters:
* The unsigned char array of the path to copy.
* The starting index of the path in its array.
* The length of the path.
* The entry's mode of operation as an 
	std::fs::FileModes or std::fs::FolderModes 
	value. 
* Either nullptr, or a pointer to a "void(
	std::ApplicationInstance, std::fs::Entry*,
	unsigned int)" function that will be called 
	after the requested operation was completed.
* The cursor's position as an unsigned int.
* The parameters to be used by the 
	requested operation as a void*.

Returns: void.

```
/*In Main::main.*/
file.set("tmp://tut/Year.md", 0, 17, 
	std::fs::FileModes::read,
	onOpened, 0, &parameters);
```

## "write" member function:

Requests to write from an std::ds::BufferView 
a sequence of unsigned char values to the file 
starting at the cursor's position, and increases 
the cursor with the number of values written.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
/*Change "read" to "write" in Main::main.*/

/*Change Main::onOpened.*/
app.main.parameters.data = "2025";
app.main.parameters.size = 4;
file->callback = onReadOrWrite;
file->write(app);
```

## "writeCall" member function:

Requests to write from an std::fs::Call 
a sequence of unsigned char values to the file 
starting at the cursor's position, and increases 
the cursor with the number of values written.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
class WriteCall : std::fs::Call {
	WriteCall(){
		call = (void())get;
	}
	static unsigned char get(
		std::fs::Call* call, 
		unsigned int cursor){
		switch (cursor){
			case 0:
				return '2';
			case 1:
				return '0';
			case 2:
				return '2';
			case 3:
				return '5';
		}
	}
}

/*Change "std::ds::BufferView" 
	to "WriteCall" in Main.*/

/*Change "read" to "write" in Main::main.*/

/*Change Main::onOpened.*/
app.main.parameters.size = 4;
file->callback = onReadOrWrite;
file->writeCall(app);
```

## "writeMove" member function:

Requests to write an std::ds::Buffer 
or move if it can instead of copying, to the file 
starting at the cursor's position, and increases 
the cursor with the number of values written.

Parameters:
The std::ApplicationInstance aexcl object.

Returns: true, if no immediate error, 
false otherwise.

```
/*Change "read" to "write" in Main::main.*/

/*Change "std::ds::BufferView" 
	to "std::ds::Buffer" in Main.*/

/*Change Main::onOpened.*/
std::arr::Uchar::copy(
	app.main.parameters.create(4), 0, 
	"2025", 0, 4);
file->callback = onReadOrWrite;
file->writeMove(app);

/*In Main::onReadOrWrite.*/
unsigned char[] data = app.main.parameters.data;
/*nullptr if moved.*/
```

# Software license

Copyright (c) 2021-2022, 2024-2025
SWARMBJECT contributors

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

Copyright (c) 2021-2022, 2024-2025
SWARMBJECT contributors

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