# "std::str::DString" class:

Used to create strings in unsigned char arrays as 
objects, where the length of the string is expected 
to be changing, thus they are dynamic strings.

## "capacity" data member:

In order so that a new array doesn't have to be 
created each time when the length of the string 
changes, instead an array with a greater capacity 
might be created than what is currently needed,
thus a new array has to be created only when enough 
characters are inserted so that a greater capacity 
is needed. Stored as an unsigned int, including 
the ending 0 unsigned char.

```
std::str::DString string;
unsigned int capacity = string.capacity; /*0*/
```

## "data" data member:

The contained data as an unsigned char array,
if direct manipulation is needed, ending 
with a 0 unsigned char.

```
std::str::DString string;
string.addCString("This is a string.");
unsigned char[] data = string.data;
unsigned char letter = data[0]; /*'T'*/
letter = data[1]; /*'h'*/
```
	
## "length" data member:

The number of unsigned chars of the string, 
excluding the ending 0 unsigned char. This 
is not nessesary the same as the number of 
characters in the string, as with UTF-8, a 
character can use 1-4 unsigned chars.

```
std::str::DString string;
string.addCString("2021");
unsigned int length = string.length; /*4*/
```

## "add" member function:

Inserts a substring to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.

Returns: void.

```
std::str::DString string;
string.add("2021", 0, 4);
/*"2021"*/
```

## "addChar" member function:

Inserts a character to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The character to insert.
* The number of times to insert the character.

Returns: void.

```
std::str::DString string;
string.add("20", 0, 2);
string.addChar('2', 2);
/*"2022"*/
```

## "addCString" member function:

Inserts a 0 ended unsigned char array string 
to the DString's end. This might require creating 
a new array and copy all the unsigned chars due 
to the capacity, making the usage of the previous 
data member not valid.

Parameters:
* The 0 ended unsigned char array string to insert.

Returns: void.

```
std::str::DString string;
string.addCString("20");
string.addCString("21");
/*"2021"*/
```

## "addDString" member function:

Inserts a DString to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* A pointer to the DString to insert.

Returns: void.

```
std::str::DString year;
year.addCString("21");
std::str::DString string;
string.addCString("20");
string.addDString(&year);
/*"2021"*/
```

## "addReplace" member function:

Inserts a string, with all occurences of another 
given string replaced, to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.
Currently does not support if the inserted string 
is a substring of the DString.

Parameters:
* The 0 ended unsigned char array string to insert.
* The string to replace, as a 0 ended 
unsigned char array.
* The string to replace with, as a 0 ended 
unsigned char array.

Returns: void.

```
std::str::DString string;
string.addReplace("2021", "21", "20");
/*"2020", as "21" is replaced with "20".*/
```

## "addString" member function:

Inserts an std::str::String to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* A pointer to the std::str::String to insert.

Returns: void.

```
std::str::String year;
year.setCString("21");
std::str::DString string;
string.addCString("20");
string.addString(&year);
/*"2021"*/
```

## "addSubReplace" member function:

Inserts a substring, with all occurences of another 
given substring replaced, to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.
* The array of the substring to replace.
* The starting index of the substring to replace 
in its array.
* The length of the substring to replace.
* The array of the substring to replace with.
* The starting index of the substring to replace 
with in its array.

Returns: void.

```
std::str::DString string;
string.addSubReplace(
	"2021", 0, 4, 
	"21", 0, 2, 
	"20", 0, 2);
/*"2020", as "21" is replaced with "20".*/
```

## "addUint" member function:

Inserts an unsigned int to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The unsigned int to insert.
* The number's base to insert, as in std::NumberBases.

Returns: void.

```
std::str::DString string;
string.addUint(2021,
	std::NumberBases::decimal);
/*"2021"*/
```

## "addView" member function:

Inserts an std::str::View to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* A pointer to the std::str::View to insert.

Returns: void.

```
std::str::View year;
year.setCString("21");
std::str::DString string;
string.addCString("20");
string.addView(&year);
/*"2021"*/
```

## "clear" member function:

Sets the DString's length to 0.

Returns: void.

```
std::str::DString string;
string.addCString("2021");
string.clear();
unsigned int length = string.length; /*0*/
```

## "compare" member function:

Compares the DString to a substring.

Parameters:
* The unsigned char array of the 
substring to compare with.
* The starting index of the substring 
to compare with in its array.
* The length of the substring to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::DString first;
first.addCString("YEAR");
unsigned char const[] second = "year";

unsigned char compare = first.compare(
	second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compare(
	second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "compareCString" member function:

Compares the DString to a 0 ended 
unsigned char array string.

Parameters:
* The 0 ended unsigned char 
array string to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::DString first;
first.addCString("YEAR");
unsigned char const[] second = "year";

unsigned char compare = 
	first.compareCString(second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareCString(second, &cmp);
/*std::Compare::equal.*/
```

## "compareDString" member function:

Compares the DString to another std::str::DString.

Parameters:
* A pointer to the DString to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::DString first;
first.addCString("YEAR");
std::str::DString second;
second.addCString("year");

unsigned char compare = 
	first.compareDString(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareDString(&second, &cmp);
/*std::Compare::equal.*/
```

## "compareString" member function:

Compares the DString to an std::str::String.

Parameters:
* A pointer to the String to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::DString first;
first.addCString("YEAR");
std::str::String second;
second.setCString("year");

unsigned char compare = 
	first.compareString(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareString(&second, &cmp);
/*std::Compare::equal.*/
```

## "compareView" member function:

Compares the DString to an std::str::View.

Parameters:
* A pointer to the std::str::View to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::DString first;
first.addCString("YEAR");
std::str::View second;
second.setCString("year");

unsigned char compare = 
	first.compareView(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareView(&second, &cmp);
/*std::Compare::equal.*/
```

## "copy" member function:

Copy a substring to the DString, by 
replacing the characters.

Parameters:
* The index in the DString to copy to.
* The unsigned char array of 
the substring to copy from.
* The starting index of the substring 
to copy from with in its array.
* The length of the substring to copy from.

Returns: void.

```
std::str::DString string;
string.addCString("2021");
string.copy(2, "20", 0, 2);
/*"2020", as "21" is replaced with "20".*/
```

## "create" member function:

Sets the DString with empty space to set 
manually. This might require creating a 
new array due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The size of the DString to create.

Returns: the DString data as unsigned char[].

```
std::str::DString string;
unsigned char[] data = string.create(2);
data[0] = '2';
data[1] = '1';
```

## "erase" member function:

Erases from the DString. This requires 
shifting all the unsigned chars after it.

Parameters:
* The starting index to erase from.
* The number of unsigned chars to erase.

Returns: void.

```
std::str::DString string;
string.addCString("2021");
string.erase(0, 2);
/*"21"*/
```

## "find" member function:

Finds the first occurence of a substring 
in the DString.

Parameters:
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* The starting index to search from in the DString.
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
std::str::DString first;
first.addCString("YEAR");
unsigned char const[] second = "year";

unsigned int position = first.findLast(
	second, 0, 4, 0, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = first.findLast(
	second, 0, 4, 0, &cmp); /*1*/
```

## "findChar" member function:

Finds the first occurence of a character 
in the DString.

Parameters:
* The character to find.
* The starting index to search from in the DString.
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
std::str::DString first;
first.addCString("YEAR");
unsigned char second = 'y';

unsigned int position = first.findChar(
	second, 0, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCharCI;
position = first.findChar(second, 0, &cmp); /*1*/
```

## "findLast" member function:

Finds the first occurence of a substring, but 
starting backwards from the end of the DString.

Parameters:
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* The index + 1 position to 
search from in the DString.
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
std::str::DString first;
first.addCString("YEAR");
unsigned char const[] second = "year";

unsigned int position = first.findLast(
	second, 0, 4, first.length, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCI;
position = first.findLast(
	second, 0, 4, first.length, &cmp); /*1*/
```

## "findLastChar" member function:

Finds the first occurence of a character, but 
starting backwards from the end of the DString.

Parameters:
* The character to find.
* The index + 1 position to 
search from in the DString.
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
std::str::DString first;
first.addCString("YEAR");
unsigned char second = 'y';

unsigned int position = first.findLastChar(
	second, first.length, nullptr); /*0*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::equalsCharCI;
position = first.findLastChar(
	second, first.length, &cmp); /*1*/
```

## "grow" member function:

Grows the DString, with empty space to set manually. 
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The ammount to grow with.

Returns: the DString data as unsigned char[].

```
std::str::DString string;
string.add("20", 0, 2);
unsigned char[] data = string.grow(2);
data[2] = '2';
data[3] = '1';
/*"2021"*/
```

## "insert" member function:

Inserts a substring to the DString. This 
requires shifting all the unsigned chars after 
it or creating a new array and copy all the 
unsigned chars due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The index in the DString to insert at.
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.

Returns: void.

```
std::str::DString string;
string.addCString("21");
string.insert(0, "20", 0, 2);
/*"2021"*/
```

## "insertChar" member function:

Inserts a character to the DString. This 
requires shifting all the unsigned chars after 
it or creating a new array and copy all the 
unsigned chars due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The index in the DString to insert at.
* The character to insert.
* The number of times to insert the character.

Returns: void.

```
std::str::DString string;
string.push('1');
string.insertChar(0, '2', 1);
/*"21"*/
```

## "move" member function:

Moves the data from another std::str::DString.
The previous data is deleted.

Parameters:
* A pointer to the DString to move from.

Returns: void.

```
std::str::DString first;
first.addCString("2020");
std::str::DString second;
second.addCString("2021");
first.move(&second);
/*first="2021", second=""*/
```

## "push" member function:

Inserts a character to the DString's end.
This might require creating a new array and copy 
all the unsigned chars due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The character to insert.

Returns: void.

```
std::str::DString string;
string.push('2');
string.push('1');
/*"21"*/
```

## "reserve" member function:

Increases the capacity of the DString. This 
requires creating a new array and copy all 
the unsigned chars, making the usage of the 
previous data member not valid.

Parameters:
* The new capacity, including 
the ending 0 unsigned char.

Returns: void.

```
std::str::DString string;
string.reserve(2);
unsigned int capacity = string.capacity; /*2*/
```

## "set" member function:

Sets the DString to be a copy of a substring.
Should work even if it is a substring of the 
DString. This might require creating a new array 
due to the capacity, making the usage of the 
previous data member not valid.

Parameters:
* The unsigned char array of the substring to copy.
* The starting index of the substring to copy 
in its array.
* The length of the substring to copy.

Returns: void.

```
std::str::DString string;
string.set("2021", 0, 4);
/*"2021"*/
```

## "setChar" member function:

Sets the DString to be a copy of a character.
This might require creating a new array 
due to the capacity, making the usage of 
the previous data member not valid.

Parameters:
* The character to copy.
* The number of times to copy the character.

Returns: void.

```
std::str::DString string;
string.setChar('2', 2);
/*"22"*/
```

## "setCString" member function:

Sets the DString to be a copy of a 0 ended 
unsigned char array string. This might 
require creating a new array due to the 
capacity, making the usage of the previous 
data member not valid.

Parameters:
* The 0 ended unsigned char array string.

Returns: void.

```
std::str::DString string;
string.setCString("2021");
/*"2021"*/
```

## "setDString" member function:

Sets the DString to be a copy of another 
std::str::DString. This might require creating 
a new array due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* A pointer to the DString to copy.

Returns: void.

```
std::str::DString year;
year.addCString("2021");
std::str::DString string;
string.setDString(&year);
/*"2021"*/
```

## "setString" member function:

Sets the DString to be a copy of an 
std::str::String. This might require creating 
a new array due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* A pointer to the std::str::String to copy.

Returns: void.

```
std::str::String year;
year.setCString("2021");
std::str::DString string;
string.setString(&year);
/*"2021"*/
```

## "setView" member function:

Sets the DString to be a copy of an 
std::str::View. This might require creating 
a new array due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* A pointer to the std::str::View to copy.

Returns: void.

```
std::str::View year;
year.setCString("2021");
std::str::DString string;
string.setView(&year);
/*"2021"*/
```

## "shift" member function:

Shifts rightwise the unsigned chars of the 
DString, to create an empty space to set 
manually. This might require creating a new 
array due to the capacity, making the usage 
of the previous data member not valid.

Parameters:
* The index in the DString to shift from.
* The ammount to shift with.

Returns: the DString data as unsigned char[].

```
std::str::DString string;
string.push('1');
unsigned char[] data = string.shift(0, 1);
data[0] = '2';
/*"21"*/
```

## "shrink" member function:

Decreases the capacity of the DString. This 
requires creating a new array and copy the 
remaining unsigned chars, making the usage 
of the previous data member not valid.

Parameters:
* The new capacity, including 
the ending 0 unsigned char.

Returns: void.

```
std::str::DString string;
string.addCString("2021");
string.shrink(3);
unsigned int capacity = string.capacity; /*3*/
unsigned int size = array.size; /*2 as "20".*/
```

## "trim" member function:

Decreases the length of the DString.

Parameters:
* The new length.

Returns: void.
	
```
std::str::DString string;
string.addCString("2021");
string.trim(2);
/*"20"*/
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