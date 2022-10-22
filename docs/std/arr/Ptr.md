# "std::arr::Ptr" class:

Static functions to work with pointer arrays.

## "compare" static function:

Compares two same sized pointer subarrays.

Parameters:
* The pointer array of the first subarray.
* The starting index of the first subarray in the array.
* The pointer array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the subarrays.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
unsigned char compare = std::arr::Ptr::compare(
	years, 1, years, 0, 1, compare);
/*std::Compare::greater as 2021 > 2020.*/
```

## "compareRange" static function:

Compares two possibly different sized 
pointer subarrays.

Parameters:
* The pointer array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The pointer array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
unsigned char compare = std::arr::Ptr::compareRange(
	years, 1, 1, years, 0, 1, compare);
/*std::Compare::greater as 2021 > 2020.*/
```

## "copy" static function:

Copy pointers from an array to another.
Works even between the same array.
	
Parameters:
* The array to copy to.
* The starting index of the array to copy to.
* The array to copy from.
* The starting index of the array to copy from.
* The number of pointers to copy.

Returns: void.

```
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
int*[] values = new int*[2];
std::arr::Ptr::copy(values, 0, years, 0, 2);
/*values=&2020,&2021.*/
```

## "ends" static function:

Compares the end of a pointer subarray, 
to a pointer subarray.

Parameters:
* The pointer array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The pointer array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
unsigned char compare = std::arr::Ptr::ends(
	years, 0, 2, years, 1, 1, compare);
/*std::Compare::equal.*/
```
	
## "find" static function:

Finds the first occurence of a pointer 
in a pointer array.

Parameters:
* The pointer array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The pointer value to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the pointer.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2021;
years[1] = new int;
*years[1] = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Ptr::find(
		years, 0, 2, &find, compare); /*1*/
```

## "findLast" static function:

Finds the first occurence of a pointer 
but starting backwards in the pointer array.

Parameters:
* The pointer array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The pointer value to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the pointer.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2021;
years[1] = new int;
*years[1] = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Ptr::findLast(
		years, 0, 2, &find, compare); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards in the pointer array.

Parameters:
* The pointer array to search in.
* The ending index to search until in the array.
* The size from the ending index to search in.
* The pointer array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting pointer.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2021;
years[1] = new int;
*years[1] = 2021;
unsigned int position = 
	std::arr::Ptr::findLastRange(
		years, 0, 2, years, 0, 1, compare); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in a pointer array.

Parameters:
* The pointer array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The pointer array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting pointer.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2021;
years[1] = new int;
*years[1] = 2021;
unsigned int position = 
	std::arr::Ptr::findRange(
		years, 0, 2, years, 0, 1, compare); /*1*/
```

## "findSorted" member function:

Finds a pointer in a pointer array, 
if the array is sorted.

Parameters:
* The pointer array to search in.
* The starting index to search from in the array.
* The size from the starting index to search in.
* The pointer value to find.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns an std::Compare value.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
static unsigned char compare(
	void* element, void* find){
	return std::val::Int::compare(
		 *(int*)element, *(int*)find);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
int find = 2021;
unsigned int position = 
	std::arr::Ptr::findSorted(
		years, 0, 2, &find, compare); /*2*/
```

## "insert" member function:

Returns the index where a pointer value 
could be inserted, if the array is sorted.

* The pointer array of a subarray.
* The starting index of the subarray.
* The size of the subarray.
* The pointer value to insert.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to insert 
and returns an std::Compare value.

Returns: unsigned int.

```
static unsigned char compare(
	void* element, void* find){
	return std::val::Int::compare(
		 *(int*)element, *(int*)find);
}

/*In some function:*/
int*[] years = new int*[1];
years[0] = new int;
*years[0] = 2020;
int insert = 2021;
unsigned int position = 
	std::arr::Ptr::insert(
		years, 0, 1, &insert, compare); /*1*/
```

## "replacedSize" static function:

Returns the size of a pointer array,
if all occurences of a subarray would be replaced.

Parameters:
* The pointer array to replace in.
* The starting index of the array to replace in.
* The size of the array to replace in.
* The subarray to replace.
* The starting index of the subarray to replace 
in its array.
* The size of the subarray to replace.
* The size of the subarray to replace with.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: unsigned int.

```
static unsigned char compare(
	void* find, void* element){
	if (*(int*)find == *(int*)element)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int* year = new int;
*year = 2021;
int*[] years = new int*[2];
years[0] = year;
years[1] = year;
unsigned int size = 
	std::arr::Ptr::replacedSize(
		years, 0, 2, 
		years, 0, 1, 
		2, compare);
	/*2, as the length of for example &2020,&2020.*/
```
	
## "reverse" static function:

Reverses a subarray of a pointer array.
	
Parameters:
* The pointer array to reverse in.
* The starting index of the subarray to reverse.
* The size of the subarray to reverse.

Returns: void.

```
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
std::arr::Ptr::reverse(years, 0, 2);
/*&2021,&2020.*/
```

## "set" static function:

Copy a pointer to the array.

Parameters:
* The array to copy to.
* The starting index of the array to copy to.
* The number of times to copy the pointer.
* A pointer to copy.

```
int*[] years = new int*[2];
int* year = new int;
*year = 2021;
std::arr::Ptr::set(years, 0, 2, year);
/*&2021,&2021.*/
```
	
## "setReplace" static function:

Copy a subarray to a pointer array, with 
all occurences of another given subarray replaced.
	
Parameters:
* The pointer array to copy to.
* The starting index of the array to copy to.
* The pointer array to copy.
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
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.

Returns: void.

```
static unsigned char compare(
	void* find, void* element){
	if (*(int*)find == *(int*)element)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
int*[] values = new int*[2];
int* year = new int;
*year = 2021;
int*[] years = new int*[2];
years[0] = year;
years[1] = year;
int*[] replace = new int*[1];
replace[0] = new int;
*replace[0] = 2020;
std::arr::Ptr::setReplace(
	values, 0,
	years, 0, 2, 
	years, 0, 1, 
	replace, 0, 1, compare);
/*&2020,&2020, as &2021, 
	is replaced with &2020.*/
```
	
## "sort" static function:

Sorts a subarray of a pointer array.

Parameters:
* The pointer array to sort in.
* The starting index of the subarray to sort.
* The size of the subarray to sort.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements and returns an std::Compare value.

Returns: void.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2021;
years[1] = new int;
*years[1] = 2020;
std::arr::Ptr::sort(
	years, 0, 2, compare);
/*&2020,&2021.*/
```

## "starts" static function:

Compares the start of a pointer subarray, 
to a pointer subarray.

Parameters:
* The pointer array of the first subarray.
* The starting index of the first subarray in the array.
* The size of the first subarray.
* The pointer array of the second subarray.
* The starting index of the second subarray in the array.
* The size of the second subarray.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given first subarray 
element with any of the second subarray 
elements and returns an std::Compare value.

Returns: an std::Compare value.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
unsigned char compare = std::arr::Ptr::starts(
	years, 0, 2, years, 0, 1, compare);
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