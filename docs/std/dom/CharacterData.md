# "std::dom::CharacterData" class:

Static functions to work with DOM character data.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node text;
		std::dom::Text::create(
			&document, &text, "2021", 0, 4);
	}
}
```

## "appendData" static function:

Appends to the character data.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.

Returns: void.

```
/*In Main::main.*/
std::dom::CharacterData::appendData(
	&text, "2021", 0, 4);
/*"20212021"*/
```

## "deleteData" static function:

Deletes from the character data.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The starting UTF-8 index to erase from.
* The number of UTF-8 unsigned chars to erase.

Returns: void.

```
/*In Main::main.*/
std::dom::CharacterData::deleteData(
	&text, 2, 2);
/*"21"*/
```

## "getData" static function:

Copy the character data to an array.
		
Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The unsigned char array to copy to.
* The starting index of the array to copy to.

Returns: the length of the character data.

```
/*In Main::main.*/
unsigned int length = 
	std::dom::CharacterData::getData(
		&text, nullptr, 0);
std::str::DString string;
std::dom::CharacterData::getData(
	&text, string.create(length), 0);
/*"2021"*/
```

## "getDataDString" static function:

Inserts a character data 
to an std::str::DString's end.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* A pointer an std::str::DString.

Returns: void.

```
/*In Main::main.*/
std::str::DString string;
std::dom::CharacterData::getDataDString(
	&text, &string);
/*"2021"*/
```

## "getLength" static function:

Gets the number of UTF-8 unsigned chars of the 
character data, without an ending 0 unsigned 
char. This is not nessesary the same as the 
number of characters in the character data, as 
with UTF-8, a character can use 1-4 unsigned chars.

Parameters:
* A pointer to the character data,
as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int length = 
	std::dom::CharacterData::getLength(
		&text); /*4*/
```

## "insertData" static function:

Inserts a substring to the character data.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The UTF-8 index in the character data to insert at.
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.

Returns: void.

```
/*In Main::main.*/
std::dom::CharacterData::insertData(
	&text, 4, "2021", 0, 4);
/*"20212021"*/
```

## "setData" static function:

Sets the character data to be a 
copy of a substring.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The unsigned char array of the substring to copy.
* The starting index of the substring to copy 
in its array.
* The length of the substring to copy.

Returns: void.

```
/*In Main::main.*/
std::dom::CharacterData::setData(
	&text, "21", 0, 2);
/*"21"*/
```

## "substringData" static function:

Copy a substring of the 
character data to an array.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* The starting UTF-8 index to copy from.
* The number of UTF-8 unsigned chars to copy.
* The unsigned char array to copy to.
* The starting index of the array to copy to.

Returns: the length of the substring.

```
/*In Main::main.*/
unsigned int length = 
	std::dom::CharacterData::substringData(
		&text, 2, 2, nullptr, 0);
std::str::DString string;
std::dom::CharacterData::substringData(
	&text, 2, 2, string.create(length), 0);
/*"21"*/
```

## "substringDataDString" static function:

Inserts a substring of the character data 
to an std::str::DString's end.

Parameters:
* A pointer to the character data,
as an std::dom::Node.
* A pointer an std::str::DString.
* The starting UTF-8 index to copy from.
* The number of UTF-8 unsigned chars to copy.

Returns: void.

```
/*In Main::main.*/
std::str::DString string;
std::dom::CharacterData::substringDataDString(
	&text, &string, 2, 2);
/*"21"*/
```

# Software license

Copyright (c) 2021, 2024 SWARMBJECT contributors

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

Copyright (c) 2021, 2024 SWARMBJECT contributors

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