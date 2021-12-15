# "std::str::String" class:

Used to create strings in unsigned char 
arrays as objects, where the length of 
the string is not expected to be changing.

## "data" data member:

The contained data as an unsigned char array,
if direct manipulation is needed, ending 
with a 0 unsigned char.

```
std::str::String string;
string.setCString("This is a string.");
unsigned char const[] data = string.data;
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
std::str::String string;
string.setCString("2021");
unsigned int length = string.length; /*4*/
```

## "clear" member function:

Clears the string to its initial state. As 
it deletes the contained array, usage of 
the previous data member is not valid.

Returns: void.

```
std::str::String string;
string.setCString("2021");
string.clear();
unsigned int length = string.length; /*0*/
```
	
## "compare" member function:

Compares the String to a substring.

Parameters:
* The unsigned char array of the 
substring to compare with.
* The starting index of the substring 
to compare with in its array.
* The length of the substring to compare with.

Returns: an std::Compare value.

```
std::str::String first;
first.setCString("first string");
unsigned char const[] second = "second string";
unsigned char compare = first.compare(second, 
	0, std::str::CString::length(second, 0));
/*std::Compare::less, as 'f' < 's'.*/
```
	
## "compareCString" member function:

Compares the String to a 0 ended 
unsigned char array string.

Parameters:
* The 0 ended unsigned char 
array string to compare with.

Returns: an std::Compare value.

```
std::str::String string;
string.setCString("first string");
unsigned char const[] second = "second string";
unsigned char compare = 
	string.compareCString(second);
/*std::Compare::less, as 'f' < 's'.*/
```

## "compareDString" member function:

Compares the String to an std::str::DString.

Parameters:
* A pointer to the DString to compare with.

Returns: an std::Compare value.

```
std::str::String first;
first.setCString("first string");
std::str::DString second;
first.addCString("second string");
unsigned char compare = 
	first.compareDString(&second);
/*std::Compare::less, as 'f' < 's'.*/
```

## "compareString" member function:

Compares the String to another std::str::String.

Parameters:
* A pointer to the String to compare with.

Returns: an std::Compare value.

```
std::str::String first;
first.setCString("first string");
std::str::String second;
second.setCString("second string");
unsigned char compare = first.compareString(&second);
/*std::Compare::less, as 'f' < 's'.*/
```

## "compareView" member function:

Compares the String to an std::str::View.

Parameters:
* A pointer to the std::str::View to compare with.

Returns: an std::Compare value.

```
std::str::String first;
first.setCString("first string");
std::str::View second;
second.setCString("second string");
unsigned char compare = first.compareView(&second);
/*std::Compare::less, as 'f' < 's'.*/
```

## "copy" member function:

Copy a substring to the String, by 
replacing the characters.

Parameters:
* The index in the String to copy to.
* The unsigned char array of 
the substring to copy from.
* The starting index of the substring 
to copy from with in its array.
* The length of the substring to copy from.

Returns: void.

```
std::str::String string;
string.setCString("2021");
string.copy(2, "20", 0, 2);
/*"2020", as "21" is replaced with "20".*/
```

## "erase" member function:

Erases from the String. As it creates a new array 
and copy the remaining unsigned chars, usage of 
the previous data member is not valid.

Parameters:
* The starting index to erase from.
* The number of unsigned chars to erase.

Returns: void.

```
std::str::String string;
string.setCString("2021");
string.erase(0, 2);
/*"21"*/
```

## "find" member function:

Finds the first occurence of a character 
in the String.

Parameters:
* The character to find.
* The starting index to search from in the String.

Returns: 0, if not found, otherwise the 
index + 1 position of the character.

```
std::str::String string;
string.setCString("2020");
unsigned int position = 
	string.find('2', 0); /*1*/
```

## "findLast" member function:

Finds the first occurence of a character, but 
starting backwards from the end of the String.

Parameters:
* The character to find.
* The index + 1 position to 
search from in the DString.

Returns: 0, if not found, otherwise the 
index + 1 position of the character.

```
std::str::String string;
string.setCString("2020");
unsigned int position = 
	string.findLast('2', string.length); /*3*/
```

## "findLastRange" member function:

Finds the first occurence of a substring, but 
starting backwards from the end of the String.

Parameters:
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* The index + 1 position to 
search from in the DString.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
std::str::String string;
string.setCString("2020");
unsigned int position = string.findLastRange(
	"20", 0, 2, string.length); /*3*/
```

## "findRange" member function:

Finds the first occurence of a substring 
in the String.

Parameters:
* The unsigned char array of the substring to find.
* The starting index of the substring to find 
in its array.
* The length of the substring to find.
* The starting index to search from in the String.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting character.

```
std::str::String string;
string.setCString("2020");
unsigned int position = 
	string.findRange("20", 0, 2, 0); /*1*/
```

## "insert" member function:

Inserts a substring to the String. As it creates 
a new array and copy all the unsigned chars, 
usage of the previous data member is not valid.

Parameters:
* The index in the String to insert at.
* The unsigned char array of the substring to insert.
* The starting index of the substring to insert 
in its array.
* The length of the substring to insert.

Returns: void.

```
std::str::String string;
string.setCString("21");
string.insert(0, "20", 0, 2);
/*"2021"*/
```

## "insertUint" member function:

Inserts an unsigned int to the String. As it creates 
a new array and copy all the unsigned chars, 
usage of the previous data member is not valid.

Parameters:
* The unsigned int to insert.
* The index in the String to insert at.
* The number's base to insert, as in std::NumberBases.

Returns: void.

```
std::str::String string;
string.insertUint(2021, 0,
	std::NumberBases::decimal);
/*"2021"*/
```

## "move" member function:

Moves the data from another std::str::String.
The previous data is deleted.

Parameters:
* A pointer to the String to move from.

Returns: void.

```
std::str::String first;
first.setCString("2020");
std::str::String second;
second.setCString("2021");
first.move(&second);
/*first="2021", second=""*/
```
	
## "reverse" member function:

Reverses the contained data of the String.

Returns: void.

```
std::str::String string;
string.setCString("21");
string.reverse();
/*"12"*/
```

## "set" member function:

Sets the String to be a copy of a substring.
Should work even if it is a substring of the 
String. As it creates a new array, usage 
of the previous data member is not valid.

Parameters:
* The unsigned char array of the substring to copy.
* The starting index of the substring to copy 
in its array.
* The length of the substring to copy.

Returns: void.

```
std::str::String string;
string.set("2021", 0, 4);
/*"2021"*/
```
	
## "setCString" member function:

Sets the String to be a copy of a 0 ended 
unsigned char array string. As it creates a 
new array, usage of the previous data member 
is not valid.

Parameters:
* The 0 ended unsigned char array string.

Returns: void.

```
std::str::String string;
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
std::str::String string;
string.setDString(&year);
/*"2021"*/
```

## "setLength" member function:

Changes the length of the string. As it creates 
a new array and copy all the unsigned chars, 
usage of the previous data member is not valid.

Parameters:
* The new length of the string.

Returns: void.

```
std::str::String string;
string.setLength(1);
unsigned int length = string.length; /*1*/
string.setLength(2);
length = string.length; /*2*/
```

## "setString" member function:

Sets the String to be a copy of another 
std::str::String. As it creates a new array, usage 
of the previous data member is not valid.

Parameters:
* A pointer to the String to copy.

Returns: void.

```
std::str::String year;
year.setCString("2021");
std::str::String string;
string.setString(&year);
/*"2021"*/
```
	
## "setView" member function:

Sets the String to be a copy of a substring 
that a std::str::View points to. As it 
creates a new array, usage of the previous 
data member is not valid.

Parameters:
* A pointer to the std::str::View to copy.

Returns: void.

```
std::str::View year;
year.setCString("2021");
std::str::String string;
string.setView(&year);
/*"2021"*/
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