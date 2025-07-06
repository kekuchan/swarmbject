# "std::fs::FileModes" enum:

## "append" constexpr data member:

Indicates a write-only and append-only mode. 
The file is created if it does not exists.

## "appendUpdate" constexpr data member:

Indicates a read and append-only write mode. 
The file is created if it does not exists.

## "erase" constexpr data member:

Indicates an erase the file mode.

```
class Main {
	std::fs::Entry file;
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		file.set("tmp://tut/Year.md", 0, 17, 
			std::fs::FileModes::erase,
			onErased, 0, nullptr);
		file.open(app);
	}
	static void onErased(
		std::ApplicationInstance aexcl app,
		std::fs::Entry* file,
		unsigned int error){
	}
}
```

## "gui" constexpr data member:

Indicates a show a gui for the file mode.

## "move" constexpr data member:

Indicates a move the file mode with the file's 
path to move to as an std::str::DString parameter.

```
class Main {
	std::fs::Entry file;
	std::str::DString parameters;
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		parameters.setCString(
			"tmp://tutorial/Year.md");
		file.set("tmp://tut/Year.md", 0, 17, 
			std::fs::FileModes::move, 
			onMoved, 0, &parameters);
		file.open(app);
	}
	static void onMoved(
		std::ApplicationInstance aexcl app,
		std::fs::Entry* file,
		unsigned int error){
	}
}
```

## "next" constexpr data member:

Indicates an iterate over all the entries 
in the containing folder, starting from 
the next entry after the contained file mode.

```
class Main {
	std::fs::Entry entry;
	void main(std::ApplicationInstance aexcl app){
		/*Assuming that "tmp://" already exists.*/
		entry.set("tmp://tut/Year.md", 0, 17, 
			std::fs::FileModes::next, 
			onOpened, 0, nullptr);
		entry.open(app);
	}
	static void onOpened(
		std::ApplicationInstance aexcl app, 
		std::fs::Entry* folder, 
		unsigned int error){
		folder->path; /* "tmp://tut/" */
		if (folder->state == 
			std::fs::FolderStates::none){
			/*No more entries.*/
			return;
		}
		/*Iterate over all the entries in 
			"tmp://tut/" starting from the 
			next entry after "Year.md".*/
	}
}
```

## "none" constexpr data member:

Indicates no mode.

## "read" constexpr data member:

Indicates a read-only mode. The file is 
not created if it does not exists.

```
class Main {
	
	std::fs::Entry file;
	std::ds::BufferView parameters;
	std::str::String string;
	
	void main(std::ApplicationInstance aexcl app){
		app.main.parameters.data = 
			app.main.string.create(4);
		app.main.parameters.size = 4;
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
		app.main.string; /*"2025"*/
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
## "readUpdate" constexpr data member:

Indicates a read-write mode. The file is 
not created if it does not exists.

## "write" constexpr data member:

Indicates a write-only mode. The file is 
created if it does not exists. If the file 
exists, an empty file is used instead.

```
class Main {
	
	std::fs::Entry file;
	std::ds::BufferView parameters;
	
	void main(std::ApplicationInstance aexcl app){
		app.main.parameters.data = "2025";
		app.main.parameters.size = 4;
		/*Assuming that "tmp://" already exists.*/
		file.set("tmp://tut/Year.md", 0, 17, 
			std::fs::FileModes::write, 
			onOpened, 0, &parameters);
		file.open(app);
	}
	
	static void onOpened(
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

## "writeUpdate" constexpr data member:

Indicates a read-write mode. The file is 
created if it does not exists. If the file 
exists, an empty file is used instead.

# Software license

Copyright (c) 2021, 2024-2025 
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

Copyright (c) 2021, 2024-2025 
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