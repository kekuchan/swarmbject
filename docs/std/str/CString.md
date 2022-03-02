# "std::str::CString" class:

Provides static functions for strings in unsigned 
char arrays, where the string's end is indicated 
with a 0 unsigned char.

## "charLength" static function:

Gets the length of a character, as if it were a string.
With UTF-8, a character can use 1-4 unsigned chars.

Parameters:
* The character.

Returns: unsigned char.

```
unsigned int length = 
	std::str::CString::charLength('2'); /*1*/
```
		
## "compare" static function:

Compares a string to a string.

Parameters:
* The unsigned char array of the first string.
* The starting index of the first string 
in the array.
* The unsigned char array of the second string.
* The starting index of the second string 
in the array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned char compare = std::str::CString::compare(
	first, 0, second, 0, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::compare(
	first, 0, second, 0, &cmp);
/*std::Compare::equal.*/
```

## "compareRange" static function:

Compares a string, to a substring.

Parameters:
* The unsigned char array of the string.
* The starting index of the string in the array.
* The unsigned char array of the substring.
* The starting index of the substring in the array.
* The length of the substring.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::compareRange(
		first, 0, second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::compareRange(
	first, 0, second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "find" static function:

Finds the first occurence of a string in a string.

Parameters:
* The unsigned char array of the string to search in.
* The starting index to search from in the array.
* The unsigned char array of the string to find.
* The starting index of the string to find 
in its array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::find(
		first, 0, second, 0, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::find(
	first, 0, second, 0, &cmp); /*1*/
```

## "findChar" static function:

Finds the first occurence of a character in a string.

Parameters:
* The unsigned char array of the string to search in.
* The starting index to search from in the array.
* The character to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare 
member pointing to a function that compares the 
character stored in dstStart with a character 
or more of its src member, from its starting 
index, returning std::Compare::equal if equal, 
or something else otherwise, and setting its 
starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the character.

```
unsigned char const[] first = "YEAR";
unsigned char second = 'y';

unsigned int position = 
	std::str::CString::findChar(
		first, 0, second, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCharCI;
position = std::str::CString::findChar(
	first, 0, second, &cmp); /*1*/
```

## "findRange" static function:

Finds the first occurence of a substring in a string.

Parameters:
* The unsigned char array of the string to search in.
* The starting index to search from in the array.
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::findRange(
		first, 0, second, 0, 4, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::findRange(
	first, 0, second, 0, 4, &cmp); /*1*/
```
		
## "getChar" static function:

Gets a character from a string. With UTF-8, 
a character can use 1-4 unsigned chars. In
case of an invalid UTF-8 value, 0xFFFD is 
returned, with the ending + 1 index set
to the given index + 1.

Parameters:
* The unsigned char array of the string.
* A pointer to an unsigned int construct, that 
contains an index of the character, and if it 
is not the same as the next parameter, then it 
will contain the starting index of the character.
* A pointer to an unsigned int construct, 
that will be set to contain the ending + 1 
index of the character in the array.
* The lowest index that can be used when a 
lower than the given character index is needed.
* The highest index + 1 that can be used when 
a higher than the given character index is needed.

Returns: unsigned int.

```
unsigned int start = 0;
unsigned int end;
unsigned int character = 
	std::str::CString::getChar(
		"2021", &start, &end, 0, 4);
/*character='2', start=0, end=1*/
```
		
## "getValidChar" static function:

Gets a character from a string, assuming 
that it is valid, as with UTF-8, a 
character can use 1-4 unsigned chars.

Parameters:
* The unsigned char array of the string.
* A pointer to an unsigned int construct, that 
contains an index of the character, and if it 
is not the same as the next parameter, then it 
will contain the starting index of the character.
* A pointer to an unsigned int construct, 
that will be set to contain the ending + 1 
index of the character in the array.

Returns: unsigned int.

```
unsigned int start = 0;
unsigned int end;
unsigned int character = 
	std::str::CString::getValidChar(
		"2021", &start, &end);
/*character='2', start=0, end=1*/
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
unsigned short year = std::str::CString::getUint(
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
	std::str::CString::length(string, 0); /*4*/
```

## "numberBaseToUint" static function:

Converts a number base enum value to
unsigned int base value.

Parameters:
* The base to convert.

Returns: unsigned int.

```
unsigned int base = 
	std::str::CString::numberBaseToUint(
		std::NumberBases::decimal); /*10*/
```

## "setChar" static function:

Sets a character to a string. With UTF-8, 
a character can use 1-4 unsigned chars.

Parameters:
* The unsigned char array of the string.
* The starting index to write in the array.
* The character to set.

Returns: the number of characters used while 
writing as an unsigned char.

```
unsigned char[] string = new unsigned char[2];
/*1 character and the ending 0.*/
string[1] = 0;
unsigned char chars = 
	std::str::CString::setChar(string, 0, '2');
/*chars=1, string="2"*/
```

## "setUint" static function:

Sets an unsigned int to a string.

Parameters:
* The unsigned char array of the string.
* The starting index to write in the array.
* The unsigned int to set.
* The number's base to write, as in std::NumberBases.

Returns: the number of characters used while 
writing as an unsigned int.

```
unsigned char[] string = new unsigned char[5];
/*4 characters and the ending 0.*/
string[4] = 0;
unsigned int chars = 
	std::str::CString::setUint(string, 0, 2021,
		std::NumberBases::decimal);
/*chars=4, string="2021"*/
```

## "setUintEnd" static function:

Sets an unsigned int to a string to end at a given 
index. This is faster than "setUint", as it can 
start processing the number backwards immediately.

Parameters:
* The unsigned char array of the string.
* The ending index to write in the array.
* The unsigned int to set.
* The number's base to write, as in std::NumberBases.

Returns: the number of characters used while 
writing as an unsigned int.

```
unsigned char[] string = new unsigned char[5];
/*4 characters and the ending 0.*/
string[4] = 0;
unsigned int chars = 
	std::str::CString::setUintEnd(string, 3, 2021,
		std::NumberBases::decimal);
/*chars=4, string="2021"*/
```

## "starts" static function:

Compares the start of a string, to a string.

Parameters:
* The unsigned char array of the first string.
* The starting index of the first string 
in the array.
* The unsigned char array of the second string.
* The starting index of the second string 
in the array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEARS";
unsigned char const[] second = "year";

unsigned char compare = std::str::CString::starts(
	first, 0, second, 0, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::starts(
	first, 0, second, 0, &cmp);
/*std::Compare::equal.*/
```

## "startsRange" static function:

Compares the start of a string, to a substring.

Parameters:
* The unsigned char array of the string.
* The starting index of the string in the array.
* The unsigned char array of the substring.
* The starting index of the substring in the array.
* The length of the substring.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEARS";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::startsRange(
		first, 0, second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::startsRange(
	first, 0, second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "subcompare" static function:

Compares a substring, to a string.

Parameters:
* The unsigned char array of the substring.
* The starting index of the substring in the array.
* The length of the substring.
* The unsigned char array of the string.
* The starting index of the string in the array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::subcompare(
		first, 0, 4, second, 0, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::subcompare(
	first, 0, 4, second, 0, &cmp);
/*std::Compare::equal.*/
```

## "subcompareRange" static function:

Compares a substring, to a substring.

Parameters:
* The unsigned char array of the first substring.
* The starting index of the 
first substring in the array.
* The length of the first substring.
* The unsigned char array of the second substring.
* The starting index of the 
second substring in the array.
* The length of the second substring.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::subcompareRange(
		first, 0, 4, second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::subcompareRange(
	first, 0, 4, second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "subendsRange" static function:

Compares the end of a substring, to a substring.

Parameters:
* The unsigned char array of the first substring.
* The starting index of the 
first substring in the array.
* The length of the first substring.
* The unsigned char array of the second substring.
* The starting index of the 
second substring in the array.
* The length of the second substring.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = " YEAR";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::subendsRange(
		first, 0, 5, second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::subendsRange(
	first, 0, 5, second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "subfind" static function:

Finds the first occurence of a string in a substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The starting index to search from in the array.
* The length of the substring to search in.
* The unsigned char array of the string to find.
* The starting index of the string to find 
in its array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::subfind(
		first, 0, 4, second, 0, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::subfind(
	first, 0, 4, second, 0, &cmp); /*1*/
```

## "subfindChar" static function:

Finds the first occurence of 
a character in a substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The starting index to search from in the array.
* The length of the substring to search in.
* The character to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare 
member pointing to a function that compares the 
character stored in dstStart with a character 
or more of its src member, from its starting 
index, returning std::Compare::equal if equal, 
or something else otherwise, and setting its 
starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the character.

```
unsigned char const[] first = "YEAR";
unsigned char second = 'y';

unsigned int position = 
	std::str::CString::subfindChar(
		first, 0, 4, second, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCharCI;
position = std::str::CString::subfindChar(
	first, 0, 4, second, &cmp); /*1*/
```

## "subfindLast" static function:

Finds the first occurence of a string,
but starting backwards in the substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The ending index to search until in the array.
* The length from the ending index to search in.
* The unsigned char array of the string to find.
* The starting index of the string to find 
in its array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::subfindLast(
		first, 0, 4, second, 0, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::subfindLast(
	first, 0, 4, second, 0, &cmp); /*1*/
```

## "subfindLastChar" static function:

Finds the first occurence of a character, 
but starting backwards in the substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The ending index to search until in the array.
* The length from the ending index to search in.
* The character to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare 
member pointing to a function that compares the 
character stored in dstStart with a character 
or more of its src member, from its starting 
index, returning std::Compare::equal if equal, 
or something else otherwise, and setting its 
starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the character.

```
unsigned char const[] first = "YEAR";
unsigned char second = 'y';

unsigned int position = 
	std::str::CString::subfindLastChar(
		first, 0, 4, second, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCharCI;
position = std::str::CString::subfindLastChar(
	first, 0, 4, second, &cmp); /*1*/
```

## "subfindLastRange" static function:

Finds the first occurence of a substring,
but starting backwards in a substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The ending index to search until in the array.
* The length from the ending index to search in.
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::subfindLastRange(
		first, 0, 4, second, 0, 4, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::subfindLastRange(
	first, 0, 4, second, 0, 4, &cmp); /*1*/
```

## "subfindRange" static function:

Finds the first occurence of a substring 
in a substring.

Parameters:
* The unsigned char array of the 
substring to search in.
* The starting index to search from in the array.
* The length of the substring to search in.
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning std::Compare::equal 
if equal, or something else otherwise, and 
setting their starting and ending + 1 indices.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

unsigned int position = 
	std::str::CString::subfindRange(
		first, 0, 4, second, 0, 4, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = std::str::CString::subfindRange(
	first, 0, 4, second, 0, 4, &cmp); /*1*/
```

## "substarts" static function:

Compares the start of a substring, to a string.

Parameters:
* The unsigned char array of the substring.
* The starting index of the substring in the array.
* The length of the substring.
* The unsigned char array of the string.
* The starting index of the string in the array.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEARS";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::substarts(
		first, 0, 5, second, 0, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::substarts(
	first, 0, 5, second, 0, &cmp);
/*std::Compare::equal.*/
```

## "substartsRange" static function:

Compares the start of a substring, to a substring.

Parameters:
* The unsigned char array of the first substring.
* The starting index of the 
first substring in the array.
* The length of the first substring.
* The unsigned char array of the second substring.
* The starting index of the 
second substring in the array.
* The length of the second substring.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
unsigned char const[] first = "YEARS";
unsigned char const[] second = "year";

unsigned char compare = 
	std::str::CString::substartsRange(
		first, 0, 5, second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = std::str::CString::substartsRange(
	first, 0, 5, second, 0, 4, &cmp);
/*std::Compare::equal.*/
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
	std::str::CString::uintLength(2021,
		std::NumberBases::decimal); /*4*/
```

# Software license

Copyright (c) 2021-2022 SWARMBJECT contributors

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

Copyright (c) 2021-2022 SWARMBJECT contributors

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