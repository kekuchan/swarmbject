# "std::CString" class:

Provides static functions for strings in unsigned 
char arrays, where the string's end is indicated 
with a 0 unsigned char.

## "compare" static function:

Compares a string to a string.

Parameters:
* The unsigned char array of the first string.
* The starting index of the first string in the array.
* The unsigned char array of the second string.
* The starting index of the second string in the array.

Returns: a positive char if the first string is
greater than the second string, 0 if equals, and a 
negative char otherwise.

```
unsigned char const[] first = "first string";
unsigned char const[] second = "second string";
char compare = std::CString::compare(
	first, 0, second, 0);
/*Negative, as 'f' < 's'.*/
```
		
## "compareSubstring" static function:

Compares a substring, to a string.

Parameters:
* The unsigned char array of the substring.
* The starting index of the substring in the array.
* The length of the substring.
* The unsigned char array of the string.
* The starting index of the string in the array.

Returns: a positive char if the substring is
greater than the string, 0 if equals, and a 
negative char otherwise.

```
unsigned char const[] string = "string";
char compare = std::CString::compare(
	string, 1, 1, string, 0);
/*Positive, as 't' > 's'.*/
```

## "getUint" static function:

Gets an unsigned int from a string.

Parameters:
* The unsigned char array of the string.
* The starting index of the number in the 
string's array.
* The maximum characters to read, however it also
returns at the first non digit character.
* Either nullptr, or a pointer to an unsigned int 
construct, that will contain the number of 
characters used while reading.
* The number's base, as in std::NumberBases.

Returns: unsigned int.

```
unsigned char const[] string = "2021";
unsigned short year = std::CString::getUint(
	string, 0, 4, nullptr, 
	std::NumberBases::decimal); /*2021*/
```

## "length" static function:

Counts the unsigned chars of the string, excluding the 
ending 0 unsigned char. This is not nessesary the 
same as the number of characters in the string, as 
with UTF-8, a character can use 1-4 unsigned chars.

Parameters:
* The unsigned char array of the string.
* The starting index of the string in the array.

Returns: unsigned int.

```
unsigned char const[] string = "2021";
unsigned int length = 
	std::CString::length(string, 0); /*4*/
```

## "numberBaseToUint" static function:

Converts a number base enum value to
unsigned int base value.

Parameters:
* The base to convert.

Returns: unsigned int.

```
unsigned int base = 
	std::CString::numberBaseToUint(
		std::NumberBases::decimal); /*10*/
```
	
## "setUint" static function:

Sets an unsigned int to a string.

Parameters:
* The unsigned int to set.
* The unsigned char array of the string.
* The starting index to write in the array.
* The number's base to write, as in std::NumberBases.

Returns: the number of characters used while 
writing as an unsigned int.

```
unsigned char[] string = new unsigned char[5];
/*4 characters and the ending 0.*/
string[4] = 0;
unsigned int chars = 
	std::CString::setUint(2021, string, 0, 
		std::NumberBases::decimal);
/*chars=4, string="2021"*/
```

## "setUintEnd" static function:

Sets an unsigned int to a string to end at a given 
index. This is faster than "setUint", as it can 
start processing the number backwards immediately.

Parameters:
* The unsigned int to set.
* The unsigned char array of the string.
* The ending index to write in the array.
* The number's base to write, as in std::NumberBases.

Returns: the number of characters used while 
writing as an unsigned int.

```
unsigned char[] string = new unsigned char[5];
/*4 characters and the ending 0.*/
string[4] = 0;
unsigned int chars = 
	std::CString::setUintEnd(2021, string, 3, 
		std::NumberBases::decimal);
/*chars=4, string="2021"*/
```

## "uintLength" static function:

Gets the length of an unsigned int 
as if it were a string.

Parameters:
* The unsigned int.
* The number's base as a string.

Returns: unsigned int.

```
unsigned int chars = 
	std::CString::uintLength(2021,
		std::NumberBases::decimal); /*4*/
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