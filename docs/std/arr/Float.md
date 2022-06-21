# "std::arr::Float" class:

Static functions to work with float arrays.

## "compare" static function:

Compares two same sized float subarrays.

Parameters:
* The float array of the first subarray.
* The starting index of the first subarray in the array.
* The float array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.

Returns: an std::Compare value.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
unsigned char compare = std::arr::Float::compare(
	years, 1, years, 0, 1);
/*std::Compare::greater as 20.21 > 20.20.*/
```

## "compareRange" static function:

Compares two possibly different sized 
float subarrays.

Parameters:
* The float array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The float array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
unsigned char compare = std::arr::Float::compareRange(
	years, 1, 1, years, 0, 1);
/*std::Compare::greater as 20.21 > 20.20.*/
```

## "compareValue" static function:

Compares two float values.
	
Parameters:
* The first float value.
* The second float value.

Returns: an std::Compare value.

```
unsigned char compare = 
	std::arr::Float::compareValue(20.20, 20.21);
/*std::Compare::less, as 20.20 < 20.21.*/
```

## "copy" static function:

Copy floats from an array to another.
Works even between the same array.
	
Parameters:
* The float array to copy to.
* The starting index of the array to copy to.
* The float array to copy from.
* The starting index of the array to copy from.
* The number of floats to copy.

Returns: void.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
float[] values = new float[2];
std::arr::Float::copy(values, 0, years, 0, 2);
/*values=20.20,20.21.*/
```

## "ends" static function:

Compares the end of a float subarray, 
to a float subarray.

Parameters:
* The float array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The float array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
unsigned char compare = std::arr::Float::ends(
	years, 0, 2, years, 1, 1);
/*std::Compare::equal.*/
```
	
## "find" static function:

Finds the first occurence of a float 
in a float array.

Parameters:
* The float array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The float value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the float.

```
float[] years = new float[2];
years[0] = 20.21;
years[1] = 20.21;
float find = 20.21;
unsigned int position = 
	std::arr::Float::find(
		years, 0, 2, find); /*1*/
```

## "findLast" static function:

Finds the first occurence of a float, 
but starting backwards in the float array.

Parameters:
* The float array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The float value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the float.

```
float[] years = new float[2];
years[0] = 20.21;
years[1] = 20.21;
float find = 20.21;
unsigned int position = 
	std::arr::Float::findLast(
		years, 0, 2, find); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the float array.

Parameters:
* The float array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The float array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting float.

```
float[] years = new float[2];
years[0] = 20.21;
years[1] = 20.21;
unsigned int position = 
	std::arr::Float::findLastRange(
		years, 0, 2, years, 0, 1); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in a float array.

Parameters:
* The float array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The float array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting float.

```
float[] years = new float[2];
years[0] = 20.21;
years[1] = 20.21;
unsigned int position = 
	std::arr::Float::findRange(
		years, 0, 2, years, 0, 1); /*1*/
```

## "findSorted" member function:

Finds a float in a float array, 
if the array is sorted.

Parameters:
* The float array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The float value to find.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
float find = 20.21;
unsigned int position = 
	std::arr::Float::findSorted(
		years, 0, 2, find); /*2*/
```

## "insert" member function:

Returns the index where a float value 
could be inserted, if the array is sorted.

* The float array of a subarray.
* The starting index of the subarray.
* The size of the subarray.
* The float value to insert.

Returns: unsigned int.

```
float[] years = new float[1];
years[0] = 20.20;
float insert = 20.21;
unsigned int position = 
	std::arr::Float::insert(
		years, 0, 1, insert); /*1*/
```

## "replacedSize" static function:

Returns the size of a float array.
if all occurences of a subarray would be replaced.

Parameters:
* The float array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.

Returns: unsigned int.

```
float year = 20.21;
float[] years = new float[2];
years[0] = year;
years[1] = year;
unsigned int size = 
	std::arr::Float::replacedSize(
		years, 0, 2, 
		years, 0, 1, 2);
	/*2, as the length of for example 20.20,20.20.*/
```
	
## "reverse" static function:

Reverses a subarray of a float array.
	
Parameters:
* The float array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.

Returns: void.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
std::arr::Float::reverse(years, 0, 2);
/*20.21,20.20.*/
```

## "set" static function:

Copy a float to a float array.

Parameters:
* The float array to copy to.
* The starting index of the array to copy to.
* The number of times to copy the float.
* A float to copy.

```
float[] years = new float[2];
float year = 20.21;
std::arr::Float::set(years, 0, 2, year);
/*20.21,20.21.*/
```
	
## "setReplace" static function:

Copy a subarray to a float array, with 
all occurences of another given subarray replaced.
	
Parameters:
* The float array to copy to.
* The starting index of the array to copy to.
* The float array to copy.
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
float[] values = new float[2];
float year = 20.21;
float[] years = new float[2];
years[0] = year;
years[1] = year;
float[] replace = new float[1];
*replace[0] = 20.20;
std::arr::Float::setReplace(
	values, 0,
	years, 0, 2, 
	years, 0, 1, 
	replace, 0, 1);
/*20.20,20.20, as 20.21, 
	is replaced with 20.20.*/
```
	
## "sort" static function:

Sorts a subarray of a float array.

Parameters:
* The float array to sort in.
* The starting index of the subarray to sort.
* The size of the subarray to sort.

Returns: void.

```
float[] years = new float[2];
years[0] = 20.21;
years[1] = 20.20;
std::arr::Float::sort(years, 0, 2);
/*20.20,20.21.*/
```

## "starts" static function:

Compares the start of a float subarray, 
to a float subarray.

Parameters:
* The float array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The float array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.

Returns: an std::Compare value.

```
float[] years = new float[2];
years[0] = 20.20;
years[1] = 20.21;
unsigned char compare = std::arr::Float::starts(
	years, 0, 2, years, 0, 1);
/*std::Compare::equal.*/
```
	
## "switchValue" static function:

Switch the value of two float constructs.
	
Parameters:
* A pointer to the first float construct.
* A pointer to the second float construct.

Returns: void.

```
float first = 20.21;
float second = 20.20;
std::arr::Float::switchValue(&first, &second);
/*20.20,20.21.*/
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