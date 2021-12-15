# "std::arr::Void" class:

Static functions to work with arrays.

```
class Year {
	int value;
	
	static unsigned char compare(
		void* year, void* element){
		return std::arr::Int::compareValue(
			(Year*)year->value, (Year*)element->value);
	}
	
	static unsigned char equal(
		void* year, void* element){
		if ((Year*)year->value == 
			(Year*)element->value)
			{return std::Compare::equal;}
		return std::Compare::unset;
	}
	
	static void* getElement(
		void* array, unsigned int i){
		Year[] years = (Year[])array;
		return &years[i];
	}
	
	static void setElement(
		void* set, void* element){
		int* value = (int*)set;
		Year* year = (Year*)set;
		year->value = (Year*)element->value;
	}
}
```

## "compare" static function:

Compares two same sized subarrays.

Parameters:
* The array of the first subarray.
* The starting index of the first subarray in the array.
* The array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
Year[] years = new Year[2];
years[0].value = 2020;
years[1].value = 2021;
unsigned char compare = std::arr::Void::compare(
	(void*)years, 1, (void*)years, 0, 1, 
	Year::getElement, Year::compare);
/*std::Compare::greater as 2021 > 2020.*/
```
	
## "compareRange" static function:

Compares two possibly different sized subarrays.

Parameters:
* The array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
Year[] years = new Year[2];
years[0].value = 2020;
years[1].value = 2021;
unsigned char compare = 
	std::arr::Void::compareRange(
		(void*)years, 1, 1, (void*)years, 0, 1, 
		Year::getElement, Year::compare);
/*std::Compare::greater as 2021 > 2020.*/
```
	
## "copy" static function:

Copy from an array to another.
Works even between the same array.
	
Parameters:
* The array to copy from.
* The starting index of the array to copy from.
* The array to copy to.
* The starting index of the array to copy to.
* The number of pointers to copy.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.

Returns: void.

```
Year[] years = new Year[2];
years[0].value = 2020;
years[1].value = 2021;
Year[] values = new Year[2];
std::arr::Void::copy(
	(void*)years, 0, (void*)values, 0, 2, 
	Year::getElement, Year::setElement);
/*values=2020,2021.*/
```

## "find" static function:

Finds the first occurence of an element.

Parameters:
* A pointer to an element to find.
* The array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the pointer.

```
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Void::find(
		&find, (void*)years, 0, 2, 
		Year::getElement, Year::equal); /*1*/
```
		
## "findLast" static function:

Finds the first occurence of an element,
but starting backwards in the array.

Parameters:
* A pointer to an element to find.
* The array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the pointer.

```
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Void::findLast(
		&find, (void*)years, 0, 2, 
		Year::getElement, Year::equal); /*2*/
```
	
## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the array.

Parameters:
* The array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* The array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
unsigned int position = 
	std::arr::Void::findLastRange(
		(void*)years, 0, 1, 
		(void*)years, 0, 2, 
		Year::getElement, Year::equal); /*2*/
```

## "findRange" static function:

Finds the first occurence of a 
subarray in the array.

Parameters:
* The array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* The array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
unsigned int position = 
	std::arr::Void::findRange(
		(void*)years, 0, 1, 
		(void*)years, 0, 2, 
		Year::getElement, Year::equal); /*1*/
```
	
## "findSorted" static function:

Finds an element in the array,
if the array is sorted.

Parameters:
* A pointer to an element to find.
* The array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
Year[] years = new Year[2];
years[0].value = 2020;
years[1].value = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Void::findSorted(
		&find, (void*)years, 0, 2, 
		Year::getElement, Year::equal); /*2*/
```

## "replacedSize" static function:

Returns the size of an array, if all 
occurences of a subarray would be replaced.

Parameters:
* The array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: unsigned int.

```
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
unsigned int size = 
	std::arr::Void::replacedSize(
		(void*)years, 0, 2, 
		(void*)years, 0, 1, 
		2, Year::getElement, Year::equal);
	/*2, as the length of &2020,&2020.*/
```

## "reverse" static function:

Reverses a subarray of an array.
	
Parameters:
* The array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a temporary element.

Returns: void.

```
Year[] years = new Year[2];
years[0].value = 2020;
years[1].value = 2021;
Year year;
std::arr::Void::reverse(
	(void*)years, 0, 2, Year::getElement, 
	Year::setElement, &year);
/*2021,2020.*/
```

## "setReplace" static function:

Copy a subarray to an array, with all 
occurences of another given subarray replaced.
	
Parameters:
* The array to copy to.
* The starting index of the array to copy to.
* The array to copy.
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
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: void.

```
Year[] values = new Year[2];
Year[] years = new Year[2];
years[0].value = 2021;
years[1].value = 2021;
Year[] replace = new Year[1];
replace[0] = 2020;
std::arr::Void::setReplace(
	(void*)values, 0,
	(void*)years, 0, 2, 
	(void*)years, 0, 1, 
	(void*)replace, 0, 1, Year::getElement, 
	Year::setElement, Year::equal);
/*2020,2020, as 2021, 
	is replaced with 2020.*/
```

## "switchValue" static function:

Switch the value of two constructs.
	
Parameters:
* A pointer to the first construct.
* A pointer to the second construct.

Returns: void.

```
Year first;
first.value = 2021;
Year second;
second.value = 2020;
Year year;
std::arr::Void::switchValue(&first, &second, 
	Year::setElement, &year);
/*2020,2021.*/
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