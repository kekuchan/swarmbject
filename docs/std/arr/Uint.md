# "std::arr::Uint" class:

Static functions to work with unsigned int arrays.

## "compare" static function:

Compares two same sized unsigned int subarrays.

Parameters:
* The unsigned int array of the first subarray.
* The starting index of the first subarray in the array.
* The unsigned int array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.

Returns: an std::Compare value.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned char compare = std::arr::Uint::compare(
	years, 1, years, 0, 1);
/*std::Compare::greater as 20212021 > 20202020.*/
```

## "compareRange" static function:

Compares two possibly different sized 
unsigned int subarrays.

Parameters:
* The unsigned int array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The unsigned int array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned char compare = std::arr::Uint::compareRange(
	years, 1, 1, years, 0, 1);
/*std::Compare::greater as 20212021 > 20202020.*/
```

## "copy" static function:

Copy unsigned ints from an array to another.
Works even between the same array.
	
Parameters:
* The unsigned int array to copy to.
* The starting index of the array to copy to.
* The unsigned int array to copy from.
* The starting index of the array to copy from.
* The number of unsigned ints to copy.

Returns: void.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned int[] values = new unsigned int[2];
std::arr::Uint::copy(values, 0, years, 0, 2);
/*values=20202020,20212021.*/
```

## "ends" static function:

Compares the end of an unsigned int subarray, 
to an unsigned int subarray.

Parameters:
* The unsigned int array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The unsigned int array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned char compare = std::arr::Uint::ends(
	years, 0, 2, years, 1, 1);
/*std::Compare::equal.*/
```
	
## "find" static function:

Finds the first occurence of an unsigned int 
in an unsigned int array.

Parameters:
* The unsigned int array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The unsigned int value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the unsigned int.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20212021;
years[1] = 20212021;
unsigned int find = 20212021;
unsigned int position = 
	std::arr::Uint::find(
		years, 0, 2, find); /*1*/
```

## "findLast" static function:

Finds the first occurence of an unsigned int, 
but starting backwards in the unsigned int array.

Parameters:
* The unsigned int array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The unsigned int value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the unsigned int.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20212021;
years[1] = 20212021;
unsigned int find = 20212021;
unsigned int position = 
	std::arr::Uint::findLast(
		years, 0, 2, find); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the unsigned int array.

Parameters:
* The unsigned int array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The unsigned int array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting unsigned int.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20212021;
years[1] = 20212021;
unsigned int position = 
	std::arr::Uint::findLastRange(
		years, 0, 2, years, 0, 1); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in an unsigned int array.

Parameters:
* The unsigned int array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The unsigned int array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting unsigned int.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20212021;
years[1] = 20212021;
unsigned int position = 
	std::arr::Uint::findRange(
		years, 0, 2, years, 0, 1); /*1*/
```

## "findSorted" member function:

Finds an unsigned int in an unsigned int array, 
if the array is sorted.

Parameters:
* The unsigned int array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The unsigned int value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned int find = 20212021;
unsigned int position = 
	std::arr::Uint::findSorted(
		years, 0, 2, find); /*2*/
```

## "insert" member function:

Returns the index where an unsigned int value 
could be inserted, if the array is sorted.

* The unsigned int array of a subarray.
* The starting index of the subarray.
* The size of the subarray.
* The unsigned int value to insert.

Returns: unsigned int.

```
unsigned int[] years = new unsigned int[1];
years[0] = 20202020;
unsigned int insert = 20212021;
unsigned int position = 
	std::arr::Uint::insert(
		years, 0, 1, insert); /*1*/
```

## "replacedSize" static function:

Returns the size of an unsigned int array.
if all occurences of a subarray would be replaced.

Parameters:
* The unsigned int array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.

Returns: unsigned int.

```
unsigned int year = 20212021;
unsigned int[] years = new unsigned int[2];
years[0] = year;
years[1] = year;
unsigned int size = 
	std::arr::Uint::replacedSize(
		years, 0, 2, 
		years, 0, 1, 2);
	/*2, as the length of for example 
		20202020,20202020.*/
```
	
## "reverse" static function:

Reverses a subarray of an unsigned int array.
	
Parameters:
* The unsigned int array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.

Returns: void.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
std::arr::Uint::reverse(years, 0, 2);
/*20212021,20202020.*/
```

## "set" static function:

Copy an unsigned int to an unsigned int array.

Parameters:
* The unsigned int array to copy to.
* The starting index of the array to copy to.
* The number of times to copy the unsigned int.
* An unsigned int to copy.

```
unsigned int[] years = new unsigned int[2];
unsigned int year = 20212021;
std::arr::Uint::set(years, 0, 2, year);
/*20212021,20212021.*/
```
	
## "setReplace" static function:

Copy a subarray to an unsigned int array, with 
all occurences of another given subarray replaced.
	
Parameters:
* The unsigned int array to copy to.
* The starting index of the array to copy to.
* The unsigned int array to copy.
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
unsigned int[] values = new unsigned int[2];
unsigned int year = 20212021;
unsigned int[] years = new unsigned int[2];
years[0] = year;
years[1] = year;
unsigned int[] replace = new unsigned int[1];
*replace[0] = 20202020;
std::arr::Uint::setReplace(
	values, 0,
	years, 0, 2, 
	years, 0, 1, 
	replace, 0, 1);
/*20202020,20202020, as 20212021,
	is replaced with 20202020.*/
```
	
## "sort" static function:

Sorts a subarray of an unsigned int array.

Parameters:
* The unsigned int array to sort in.
* The starting index of the subarray to sort.
* The size of the subarray to sort.

Returns: void.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20212021;
years[1] = 20202020;
std::arr::Uint::sort(years, 0, 2);
/*20202020,20212021.*/
```

## "starts" static function:

Compares the start of an unsigned int subarray, 
to an unsigned int subarray.

Parameters:
* The unsigned int array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The unsigned int array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
unsigned int[] years = new unsigned int[2];
years[0] = 20202020;
years[1] = 20212021;
unsigned char compare = std::arr::Uint::starts(
	years, 0, 2, years, 0, 1);
/*std::Compare::equal.*/
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