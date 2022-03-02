# "std::arr::Short" class:

Static functions to work with short arrays.

## "compare" static function:

Compares two same sized short subarrays.

Parameters:
* The short array of the first subarray.
* The starting index of the first subarray in the array.
* The short array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.

Returns: an std::Compare value.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
unsigned char compare = std::arr::Short::compare(
	years, 1, years, 0, 1);
/*std::Compare::less as -2021 < -2020.*/
```

## "compareRange" static function:

Compares two possibly different sized 
short subarrays.

Parameters:
* The short array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The short array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
unsigned char compare = std::arr::Short::compareRange(
	years, 1, 1, years, 0, 1);
/*std::Compare::less as -2021 < -2020.*/
```

## "compareValue" static function:

Compares two short values.

Parameters:
* The first short value.
* The second short value.

Returns: an std::Compare value.

```
unsigned char compare = 
	std::arr::Short::compareValue(-2020, -2021);
/*std::Compare::greater as -2020 > -2021.*/
```

## "copy" static function:

Copy shorts from an array to another.
Works even between the same array.
	
Parameters:
* The short array to copy to.
* The starting index of the array to copy to.
* The short array to copy from.
* The starting index of the array to copy from.
* The number of shorts to copy.

Returns: void.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
short[] values = new short[2];
std::arr::Short::copy(values, 0, years, 0, 2);
/*values=-2020,-2021.*/
```

## "ends" static function:

Compares the end of a short subarray, 
to a short subarray.

Parameters:
* The short array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The short array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
unsigned char compare = std::arr::Short::ends(
	years, 0, 2, years, 1, 1);
/*std::Compare::equal.*/
```
	
## "find" static function:

Finds the first occurence of a short 
in a short array.

Parameters:
* The short array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The short value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the short.

```
short[] years = new short[2];
years[0] = -2021;
years[1] = -2021;
short find = -2021;
unsigned int position = 
	std::arr::Short::find(
		years, 0, 2, find); /*1*/
```

## "findLast" static function:

Finds the first occurence of a short, 
but starting backwards in the short array.

Parameters:
* The short array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The short value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the short.

```
short[] years = new short[2];
years[0] = -2021;
years[1] = -2021;
short find = -2021;
unsigned int position = 
	std::arr::Short::findLast(
		years, 0, 2, find); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the short array.

Parameters:
* The short array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The short array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting short.

```
short[] years = new short[2];
years[0] = -2021;
years[1] = -2021;
unsigned int position = 
	std::arr::Short::findLastRange(
		years, 0, 2, years, 0, 1); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in a short array.

Parameters:
* The short array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The short array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting short.

```
short[] years = new short[2];
years[0] = -2021;
years[1] = -2021;
unsigned int position = 
	std::arr::Short::findRange(
		years, 0, 2, years, 0, 1); /*1*/
```

## "findSorted" member function:

Finds a short in a short array, 
if the array is sorted.

Parameters:
* The short array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The short value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
short[] years = new short[2];
years[0] = -2021;
years[1] = -2020;
short find = -2021;
unsigned int position = 
	std::arr::Short::findSorted(
		years, 0, 2, find); /*1*/
```

## "insert" member function:

Returns the index where a short value 
could be inserted, if the array is sorted.

* The short array of a subarray.
* The starting index of the subarray.
* The size of the subarray.
* The short value to insert.

Returns: unsigned int.

```
short[] years = new short[1];
years[0] = -2021;
short insert = -2020;
unsigned int position = 
	std::arr::Short::insert(
		years, 0, 1, insert); /*1*/
```

## "replacedSize" static function:

Returns the size of a short array.
if all occurences of a subarray would be replaced.

Parameters:
* The short array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.

Returns: unsigned int.

```
short year = -2021;
short[] years = new short[2];
years[0] = year;
years[1] = year;
unsigned int size = 
	std::arr::Short::replacedSize(
		years, 0, 2, 
		years, 0, 1, 2);
	/*2, as the length of for example -2020,-2020.*/
```
	
## "reverse" static function:

Reverses a subarray of a short array.
	
Parameters:
* The short array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.

Returns: void.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
std::arr::Short::reverse(years, 0, 2);
/*-2021,-2020.*/
```

## "set" static function:

Copy a short to a short array.

Parameters:
* The short array to copy to.
* The starting index of the array to copy to.
* The number of times to copy the short.
* A short to copy.

```
short[] years = new short[2];
short year = -2021;
std::arr::Short::set(years, 0, 2, year);
/*-2021,-2021.*/
```
	
## "setReplace" static function:

Copy a subarray to a short array, with 
all occurences of another given subarray replaced.
	
Parameters:
* The short array to copy to.
* The starting index of the array to copy to.
* The short array to copy.
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
short[] values = new short[2];
short year = -2021;
short[] years = new short[2];
years[0] = year;
years[1] = year;
short[] replace = new short[1];
*replace[0] = -2020;
std::arr::Short::setReplace(
	values, 0,
	years, 0, 2, 
	years, 0, 1, 
	replace, 0, 1);
/*-2020,-2020, as -2021, 
	is replaced with -2020.*/
```

## "starts" static function:

Compares the start of a short subarray, 
to a short subarray.

Parameters:
* The short array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The short array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
short[] years = new short[2];
years[0] = -2020;
years[1] = -2021;
unsigned char compare = std::arr::Short::starts(
	years, 0, 2, years, 0, 1);
/*std::Compare::equal.*/
```
	
## "switchValue" static function:

Switch the value of two short constructs.
	
Parameters:
* A pointer to the first short construct.
* A pointer to the second short construct.

Returns: void.

```
short first = -2021;
short second = -2020;
std::arr::Short::switchValue(&first, &second);
/*-2020,-2021.*/
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