# "std::ds::PtrDArray" class:

Used to create pointer containing arrays as objects, 
where the number of elements are expected to be 
changing, thus they are dynamic arrays.

## "capacity" data member:

In order so that a new array doesn't have to be 
created each time when its number of pointers 
changes, instead an array with a greater capacity 
might be created than what is currently needed,
thus a new array has to be created only when enough 
pointers are inserted so that a greater capacity is
needed. Stored as an unsigned int.

```
std::ds::PtrDArray array;
unsigned int capacity = array.capacity; /*0*/
```

## "data" data member:

The contained array of pointers. It is a 
void*[], as the PtrDArray does not know the 
actual pointer type, thus it has to be converted.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
int*[] years = (int*[])(array.data);
/*&2020,&2021*/
```

## "size" data member:

The number of elements in the array as 
an unsigned int.

```
std::ds::PtrDArray array;
unsigned int size = array.size; /*0*/
```

## "add" member function:

Inserts an element to the array's end.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* A pointer to insert.
* The number of times to insert the element.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.add(year, 2);
/*&2021,&2021*/
```

## "addRange" member function:

Inserts a subarray to the array's end.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The array of the subarray to insert.
* The starting index of the subarray to insert 
in its array.
* The size of the subarray to insert.

Returns: void.

```
std::ds::PtrDArray array;
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
array.addRange(years, 0, 2);
/*&2020,&2021*/
```

## "clear" member function:

Sets the PtrDArray's size to 0. The pointed datas 
are not deleted automatically, as they might be 
still used elsewhere.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
/*When not needed anymore:*/
delete year;
array.clear();
unsigned int size = array.size; /*0*/
```

## "compare" member function:

Compares the array to a subarray.

Parameters:
* The array of the subarray to compare with.
* The starting index of the subarray to 
compare with in its array.
* The size of the subarray to compare with.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given subarray 
element with any of the array elements 
and returns an std::Compare value.

Returns: an std::Compare value.

```
static unsigned char compare(
	void* value, void* element){
	return std::val::Int::compare(
		*(int*)value, *(int*)element);
}

/*In some function:*/
std::ds::PtrDArray array;
int*[] years = new int*[2];
int* year = new int;
*year = 2020;
array.insert(0, year, 1);
years[0] = year;
year = new int;
*year = 2021;
array.insert(0, year, 1);
years[1] = year;
array.compare(years, 0, 2, compare);
/*std::Compare::greater as 
	2021,2020 > 2020,2021.*/
```

## "copy" member function:

Copy an element to the array, by 
replacing the values.

Parameters:
* The starting index in the array to copy to.
* A pointer to copy.
* The number of times to copy the element.

Returns: void.

```
std::ds::PtrDArray array;
array.create(2);
int* year = new int;
*year = 2021;
array.copy(0, year, 2);
/*&2021,&2021*/
```

## "copyRange" member function:

Copy a subarray to the array, by 
replacing the values.

Parameters:
* The index in the array to copy to.
* The array of the subarray to copy from.
* The starting index of the subarray to 
copy from with in its array.
* The size of the subarray to copy from.

Returns: void.

```
std::ds::PtrDArray array;
int*[] years = new int*[2];
int* year = new int;
*year = 2020;
array.insert(0, year, 1);
years[0] = year;
year = new int;
*year = 2021;
array.insert(0, year, 1);
years[1] = year;
array.copyRange(0, years, 0, 2);
/*&2020,&2021*/
```

## "create" member function:

Sets the array with empty space to set 
manually. This might require creating a 
new array due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The size of the array to create.

Returns: the array data as void*[].

```
std::ds::PtrDArray array;
int*[] years = (int*[])(array.create(2));
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
/*&2020,&2021*/
```

## "erase" member function:

Erases elements from the array. This requires
shifting all the elements after it. The pointed 
data is not deleted automatically, as it might be 
still used elsewhere.

Parameters:
* The index of the first element to erase.
* The number of elements to erase.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
/*When not needed anymore:*/
delete (int*)(array.data[0]);
array.erase(0, 1);
/*&2021*/
```

## "find" static function:

Finds the first occurence of an element.

Parameters:
* A pointer to an element to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
int find = 2021;
unsigned int i = array.find(
	&find, compare, 0); /*1*/
```

## "findLast" static function:

Finds the first occurence of an element,
but starting backwards in the array.

Parameters:
* A pointer to an element to find.
* Either nullptr for pointer comparison, or 
a pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to find 
and returns std::Compare::equal 
if equal, or something else otherwise.
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
int find = 2021;
unsigned int i = array.findLast(
	&find, compare, array.size); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards from the end of the array.

Parameters:
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
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
unsigned int position = array.findLastRange(
	array.data, 0, 1, compare, array.size); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in the array.

Parameters:
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
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
static unsigned char compare(
	void* element, void* find){
	if (*(int*)element == *(int*)find)
		{return std::Compare::equal;}
	return std::Compare::unset;
}

/*In some function:*/
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
unsigned int position = array.findRange(
	array.data, 0, 1, compare, 0); /*1*/
```

## "findSorted" member function:

Finds an element, if the array is sorted.

Parameters:
* A pointer to an element to find.
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
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
int find = 2021;
unsigned int i = array.findSorted(
	&find, compare); /*2*/
```

## "getBack" member function:

Gets the last element.
	
Returns: void*.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
year = (int*)(array.getBack()); /*&2021*/
```

## "grow" member function:

Grows the array, with empty space to set manually.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The ammount to grow with.

Returns: the array data as void*[].

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
int*[] years = (int*[])(array.grow(1));
years[1] = new int;
*years[1] = 2021;
/*&2020,&2021*/
```

## "insert" member function:

Inserts an element to the array. This requires 
shifting all the elements after it or creating 
a new array and copy all the elements due to 
the capacity, making the usage of the previous 
data member not valid.

Parameters:
* The index in the array to insert at.
* A pointer to insert.
* The number of times to insert the element.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
year = new int;
*year = 2020;
array.insert(0, year, 1);
/*&2020,&2021*/
```

## "insertRange" member function:

Inserts a subarray to the array. This requires 
shifting all the elements after it or creating 
a new array and copy all the elements due to 
the capacity, making the usage of the previous 
data member not valid.

Parameters:
* The index in the array to insert at.
* The array of the subarray to insert.
* The starting index of the subarray to insert 
in its array.
* The size of the subarray to insert.

Returns: void.

```
std::ds::PtrDArray array;
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
array.insertRange(0, years, 0, 2);
/*&2020,&2021*/
```

## "insertSorted" member function:

Inserts an element to the array at a position 
to keep the array as sorted. This requires 
shifting all the elements after it or creating 
a new array and copy all the elements due to 
the capacity, making the usage of the previous 
data member not valid.

Parameters:
* A pointer to insert.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the array 
elements with the given element to insert 
and returns an std::Compare value.

Returns: void.

```
static unsigned char compare(
	void* element, void* insert){
	return std::val::Int::compare(
		*(int*)element, *(int*)insert);
}
		
/*In some function:*/
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.insertSorted(year, compare);
year = new int;
*year = 2020;
array.insertSorted(year, compare);
/*&2020,&2021*/
```

## "move" member function:

Moves the data from another std::ds::PtrDArray.
The previous data is deleted, however the 
pointed data is not deleted automatically, 
as it might be still used elsewhere.

Parameters:
* A pointer to the PtrDArray to move from.

Returns: void.

```
std::ds::PtrDArray first;
int* year = new int;
*year = 2020;
first.push(year);
std::ds::PtrDArray second;
year = new int;
*year = 2021;
second.push(year);
delete first.data[0];
first.move(&second);
/*first=&2021, second=*/
```

## "pop" member function:

Gets and removes the last element.
	
Returns: void*.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
year = (int*)(array.pop()); /*&2021*/
unsigned int size = array.size;
/*1 as &2020*/
```

## "push" member function:

Inserts an element to the array's end. This 
might require creating a new array and copy all 
the elements due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The pointer to insert.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
/*&2020,&2021*/
```

## "reserve" member function:

Increases the capacity of the array. This 
requires creating a new array and copy 
all the elements, making the usage of the 
previous data member not valid.

Parameters:
* The new capacity.

Returns: void.

```
std::ds::PtrDArray array;
array.reserve(2);
unsigned int capacity = array.capacity; /*2*/
unsigned int size = array.size; /*0*/
```
	
## "reverse" member function:

Reverses the elements of the array.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
array.reverse();
/*&2021,&2020*/
```

## "set" member function:

Sets the array to be a copy of an element.
This might require creating a new array 
due to the capacity, making the usage of 
the previous data member not valid.

Parameters:
* The pointer to copy.
* The number of times to copy the element.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.set(year, 2);
/*&2021,&2021*/
```

## "setRange" member function:

Sets the array to be a copy of a subarray.
This might require creating a new array 
due to the capacity, making the usage of 
the previous data member not valid.

Parameters:
* The array of the subarray to copy.
* The starting index of the subarray to copy 
in its array.
* The size of the subarray to copy.

Returns: void.

```
std::ds::PtrDArray array;
int*[] years = new int*[2];
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
array.setRange(years, 0, 2);
/*&2020,&2021*/
```

## "shift" member function:

Shifts rightwise the elements of the array, 
to create an empty space to set manually.
This might require creating a new array 
due to the capacity, making the usage of 
the previous data member not valid.

Parameters:
* The index in the array to shift from.
* The ammount to shift with.

Returns: the array data as void*[].

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2021;
array.push(year);
int*[] years = (int*[])(array.shift(0, 1));
years[0] = new int;
*years[0] = 2020;
/*&2020,&2021*/
```

## "shrink" member function:

Decreases the capacity of the array. This requires 
creating a new array and copy the remaining 
elements, making the usage of the previous data 
member not valid. The pointed datas are not deleted 
automatically, as they might be still used elsewhere.

Parameters:
* The new capacity.

Returns: void.

```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
/*When not needed anymore:*/
delete year;
array.shrink(1);
unsigned int capacity = array.capacity; /*1*/
unsigned int size = array.size; /*1 as &2020.*/
```

## "trim" member function:

Decreases the size of the array. The pointed datas 
are not deleted automatically, as they might be 
still used elsewhere.

Parameters:
* The new size.

Returns: void.
	
```
std::ds::PtrDArray array;
int* year = new int;
*year = 2020;
array.push(year);
year = new int;
*year = 2021;
array.push(year);
/*When not needed anymore:*/
delete year;
array.trim(1);
unsigned int size = array.size; /*1 as &2020.*/
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