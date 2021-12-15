# "std::arr::Uchar" class:

Static functions to work with unsigned char arrays.

## "compare" static function:

Compares two same sized unsigned char subarrays.

Parameters:
* The unsigned char array of the first subarray.
* The starting index of the first subarray in the array.
* The unsigned char array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.

Returns: an std::Compare value.

```
unsigned char const[] string = "string";
unsigned char compare = std::arr::Uchar::compare(
	string, 1, string, 0, 1);
/*std::Compare::greater as 't' > 's'.*/
```

## "compareRange" static function:

Compares two possibly different sized 
unsigned char subarrays.

Parameters:
* The unsigned char array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The unsigned char array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
unsigned char const[] string = "string";
unsigned char compare = std::arr::Uchar::compareRange(
	string, 1, 1, string, 0, 1);
/*std::Compare::greater as 't' > 's'.*/
```

## "compareValue" static function:

Compares two unsigned char values.
	
Parameters:
* The first unsigned char value.
* The second unsigned char value.

Returns: an std::Compare value.

```
unsigned char compare = 
	std::arr::Uchar::compareValue('t', 's');
/*std::Compare::greater as 't' > 's'.*/
```

## "copy" static function:

Copy unsigned chars from an array to another.
Works even between the same array.
	
Parameters:
* The unsigned char array to copy from.
* The starting index of the array to copy from.
* The unsigned char array to copy to.
* The starting index of the array to copy to.
* The number of unsigned chars to copy.

Returns: void.

```
unsigned char[] values = new unsigned char[4];
std::arr::Uchar::copy("2021", 0, values, 0, 4);
/*values='2','0','2','1'.*/
```
	
## "find" static function:

Finds the first occurence of an unsigned char 
in an unsigned char array.

Parameters:
* The unsigned char value to find.
* The unsigned char array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.

Returns: 0, if not found, otherwise the 
index + 1 position of the unsigned char.

```
unsigned int position = 
	std::arr::Uchar::find(
		'2', "2020", 0, 4); /*1*/
```

## "findLast" static function:

Finds the first occurence of an unsigned char, 
but starting backwards in the unsigned char array.

Parameters:
* The unsigned char value to find.
* The unsigned char array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.

Returns: 0, if not found, otherwise the 
index + 1 position of the unsigned char.

```
unsigned int position = 
	std::arr::Uchar::findLast(
		'2', "2020", 0, 4); /*3*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the unsigned char array.

Parameters:
* The unsigned char array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* The unsigned char array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting unsigned char.

```
unsigned int position = 
	std::arr::Uchar::findLastRange(
		"20", 0, 2, "2020", 0, 4); /*3*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in an unsigned char array.

Parameters:
* The unsigned char array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* The unsigned char array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting unsigned char.

```
unsigned int position = 
	std::arr::Uchar::findRange(
		"20", 0, 2, "2020", 0, 4); /*1*/
```

## "findSorted" member function:

Finds an unsigned char in an unsigned 
char array, if the array is sorted.

Parameters:
* The unsigned char value to find.
* The unsigned char array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
unsigned int position = 
	std::arr::Uchar::findSorted(
		'2', "012", 0, 3); /*3*/
```

## "getU16BE" static function:

Gets an unsigned short value from an unsigned 
char array that was stored as a big endian 
(2 unsigned chars stored left to right).

Parameters:
* The unsigned char array.
* The index of the value in the array.

Returns: unsigned short.

```
unsigned char[] buffer = new unsigned char[2];
std::arr::Uchar::setU16BE(buffer, 0, 2021);
unsigned short value =
	std::arr::Uchar::getU16BE(buffer, 0); /*2021*/
```
		
## "getU16LE" static function:

Gets an unsigned short value from an unsigned 
char array that was stored as a little endian 
(2 unsigned chars stored right to left).

Parameters:
* The unsigned char array.
* The index of the value in the array.

Returns: unsigned short.

```
unsigned char[] buffer = new unsigned char[2];
std::arr::Uchar::setU16LE(buffer, 0, 2021);
unsigned short value =
	std::arr::Uchar::getU16LE(buffer, 0); /*2021*/
```

## "getU32BE" static function:

Gets an unsigned int value from an unsigned 
char array that was stored as a big endian 
(4 unsigned chars stored left to right).

Parameters:
* The unsigned char array.
* The index of the value in the array.

Returns: unsigned short.

```
unsigned char[] buffer = new unsigned char[4];
std::arr::Uchar::setU32BE(buffer, 0, 20212021);
unsigned short value =
	std::arr::Uchar::getU32BE(buffer, 0); /*20212021*/
```

## "getU32LE" static function:

Gets an unsigned int value from an unsigned 
char array that was stored as a little endian 
(4 unsigned chars stored right to left).

Parameters:
* The unsigned char array.
* The index of the value in the array.

Returns: unsigned short.

```
unsigned char[] buffer = new unsigned char[4];
std::arr::Uchar::setU32LE(buffer, 0, 20212021);
unsigned short value =
	std::arr::Uchar::getU32LE(buffer, 0); /*20212021*/
```

## "replacedSize" static function:

Returns the size of an unsigned char array.
if all occurences of a subarray would be replaced.

Parameters:
* The unsigned char array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.

Returns: unsigned int.

```
unsigned int size = 
	std::arr::Uchar::replacedSize(
		"2021", 0, 4, 
		"21", 0, 2, 
		2);
	/*4, as the size of '2','0','2','0'.*/
```
	
## "reverse" static function:

Reverses a subarray of an unsigned char array.
	
Parameters:
* The unsigned char array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.

Returns: void.

```
unsigned char[] values = new unsigned char[2];
values[0] = '2';
values[1] = '1';
std::arr::Uchar::reverse(values, 0, 2);
/*'1','2'*/
```
	
## "setReplace" static function:

Copy a subarray to an unsigned char array, with
all occurences of another given substring replaced.
	
Parameters:
* The unsigned char array to copy to.
* The starting index of the array to copy to.
* The unsigned char array to copy.
* The starting index of the array to copy.
* The size of the array to copy.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The subarray to replace with.
* The starting index of the subarray to replace 
with in its array.
* The size of the subarray to replace with.

Returns: void.

```
unsigned char[] values = new unsigned char[4];
std::arr::Uchar::setReplace(
	values, 0,
	"2021", 0, 4, 
	"21", 0, 2, 
	"20", 0, 2);
/*'2','0','2','0', as '2','1' 
	is replaced with '2','0'.*/
```

## "setU16BE" static function:

Sets an unsigned short value to the unsigned 
char array, as a big endian (2 unsigned 
chars stored left to right).

Parameters:
* The unsigned char array.
* The index to set the value in the array.
* The unsigned short value to set.

Returns: void.

An example was already given at the 
"getU16BE" member function.

## "setU16LE" static function:

Sets an unsigned short value to the unsigned 
char array, as a little endian (2 unsigned 
chars stored right to left).

Parameters:
* The unsigned char array.
* The index to set the value in the array.
* The unsigned short value to set.

Returns: void.

An example was already given at the 
"getU16LE" member function.

## "setU32BE" static function:

Sets an unsigned int value to the unsigned 
char array, as a big endian (4 unsigned 
chars stored left to right).

Parameters:
* The unsigned char array.
* The index to set the value in the array.
* The unsigned int value to set.

Returns: void.

An example was already given at the 
"getU32BE" member function.

## "setU32LE" static function:

Sets an unsigned int value to the unsigned 
char array, as a little endian (4 unsigned 
chars stored right to left).

Parameters:
* The unsigned char array.
* The index to set the value in the array.
* The unsigned int value to set.

Returns: void.

An example was already given at the 
"getU32LE" member function.
	
## "switchValue" static function:

Switch the value of two unsigned char constructs.
	
Parameters:
* A pointer to the first unsigned char construct.
* A pointer to the second unsigned char construct.

Returns: void.

```
unsigned char first = '2';
unsigned char second = '1';
std::arr::Uchar::switchValue(&first, &second);
/*'1','2'*/
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