# "std::ds::DArray" class:

Used to create arrays as objects, where the number 
of elements are expected to be changing, thus they
are dynamic arrays.

```
/*To store int values in a dynamic array.*/
class IntDArray : std::ds::DArray {}
```

## "capacity" data member:

In order so that a new array doesn't have to be 
created each time when its number of elements 
changes, instead an array with a greater capacity 
might be created than what is currently needed,
thus a new array has to be created only when enough 
elements are inserted so that a greater capacity is
needed. Stored as an unsigned int.

```
IntDArray array;
unsigned int capacity = array.capacity; /*0*/
```

## "data" data member:

The contained array of data. It is a void*, as 
the DArray does not know its actual type, thus 
it has to be converted.

```
/*In the IntDArray class:*/

/*Required, as the DArray does not delete the 
	data automatically, as it does not know its type.*/
~IntDArray(){
	delete[] (int[])data;
}
	
int[] getData(){
	return (int[])data;
}

/*Some functions to be used by the member functions.*/
static unsigned char compareValue(
	void* value, void* element){
	return std::arr::Int::compareValue(
		*(int*)value, *(int*)element);
}
static unsigned char equal(
	void* value, void* element){
	if (*(int*)value == *(int*)element)
		{return std::Compare::equal;}
	return std::Compare::unset;
}
static void* getElement(
	void* array, unsigned int i){
	int[] ints = (int[])array;
	return &ints[i];
}
static void setElement(
	void* set, void* element){
	int* value = (int*)set;
	*value = *(int*)element;
}
static void* newArray(unsigned int size){
	return (void*)(new int[size]);
}
static void deleteArray(void* array){
	delete[] (int[])array;
}
```
	
## "size" data member:

The number of elements in the array as 
an unsigned int.

```
IntDArray array;
unsigned int size = array.size; /*0*/
```

## "add" member function:

Inserts a subarray to the array's end.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The array of the subarray to insert.
* The starting index of the subarray to insert 
in its array.
* The size of the subarray to insert.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void addInt(int[] array, 
	unsigned int i, unsigned int elements){
	add((void*)array, i, elements, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.addInt(years, 0, 2);
/*2020,2021*/
```

## "clear" member function:

Sets the array's size to 0.

Returns: void.

```
/*In some function:*/
IntDArray array;
array.pushInt(2021);
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
function that can compare the given 
subarray element with any of the array 
elements and returns an std::Compare value.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.

Returns: an std::Compare value.

```
/*In the IntDArray class:*/
void compareInt(int[] array, 
	unsigned int i, unsigned int elements){
	compare((void*)array, i, elements,
		compareValue, getElement);
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2020);
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.compareInt(years, 0, 2);
/*std::Compare::greater as 
	2021,2020 > 2020,2021.*/
```

## "copy" member function:

Copy a subarray to the array, by 
replacing the values.

Parameters:
* The index in the array to copy to.
* The array of the subarray to copy from.
* The starting index of the subarray to 
copy from with in its array.
* The size of the subarray to copy from.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.

Returns: void.

```
/*In the IntDArray class:*/
void copyInt(
	unsigned int start, int[] array, 
	unsigned int i, unsigned int elements){
	copy(start, (void*)array, i, elements,
		getElement, setElement){
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2020);
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.copyInt(0, years, 0, 2);
/*2020,2021*/
```

## "erase" member function:

Erases elements from the array. This requires
shifting all the elements after it.

Parameters:
* The index of the first element to erase.
* The number of elements to erase.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.

Returns: void.

```
/*In the IntDArray class:*/
void eraseInt(unsigned int i, 
	unsigned int elements){
	erase(i, elements, getElement, setElement);
}

/*In some function:*/
IntDArray array;
array.pushInt(2020);
array.pushInt(2021);
unsigned int size = array.size;
/*2 as 2020, 2021.*/
array.eraseInt(0, 1);
size = array.size; /*1 as 2021.*/
```

## "find" static function:

Finds the first occurence of an element.

Parameters:
* A pointer to an element to find.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntDArray class:*/
unsigned int findInt(
	unsigned int element, unsigned int i){
	return find(&element, getElement, equal, i);
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2021);
unsigned int i = array.findInt(
	2021, 0); /*1*/
```

## "findLast" static function:

Finds the first occurence of an element,
but starting backwards in the array.

Parameters:
* A pointer to an element to find.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntDArray class:*/
unsigned int findLastInt(
	unsigned int element, unsigned int i){
	return findLast(
		&element, getElement, equal, i);
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2021);
unsigned int i = array.findLastInt(
	2021, array.size); /*2*/
```

## "findLastRange" static function:

Finds the first occurence of a subarray, but 
starting backwards from the end of the array.

Parameters:
* The array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
/*In the IntDArray class:*/
unsigned int findLastRangeInt(
	int[] array, unsigned int i, 
	unsigned int elements, unsigned int start){
	return findLastRange((void*)array, i, 
		elements, getElement, equal, start){
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2021);
unsigned int position = array.findLastRangeInt(
	(int[])(array.data), 0, 1, array.size); /*2*/
```
	
## "findRange" static function:

Finds the first occurence of a subarray 
in the array.

Parameters:
* The array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns std::Compare::equal 
if equal, or something else otherwise.
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
/*In the IntDArray class:*/
unsigned int findRangeInt(
	int[] array, unsigned int i, 
	unsigned int elements, unsigned int start){
	return findRange((void*)array, i, 
		elements, getElement, equal, start){
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.pushInt(2021);
unsigned int position = array.findRangeInt(
	(int[])(array.data), 0, 1, 0); /*1*/
```

## "findSorted" member function:

Finds an element, if the array is sorted.

Parameters:
* A pointer to an element to find.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to find with any of the array 
elements and returns an std::Compare value.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntDArray class:*/
unsigned int findSortedInt(
	unsigned int element){
	return findSorted(&element, getElement, equal);
}
		
/*In some function:*/
IntDArray array;
array.pushInt(2020);
array.pushInt(2021);
unsigned int i = 
	array.findSortedInt(2021); /*2*/
```

## "insert" member function:
		
Inserts an element to the array. This requires 
shifting all the elements after it or creating 
a new array and copy all the elements due to 
the capacity, making the usage of the previous 
data member not valid.

Parameters:
* The index in the array to insert at.
* A pointer to the element to insert.
* The number of times to insert the element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void insertInt(unsigned int i, int value, 
	unsigned int elements){
	insert(i, &value, elements, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
unsigned int size = array.size;
/*1 as 2021.*/
array.insertInt(0, 2020, 1);
size = array.size;
/*2 as 2020, 2021.*/
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
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void insertRangeInt(
	unsigned int start, int[] array, 
	unsigned int i, unsigned int elements){
	insertRange(start, (void*)array, i, elements, 
		getElement, setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.insertRangeInt(0, years, 0, 2);
/*2020,2021*/
```

## "insertSorted" member function:

Inserts an element to the array at a position 
to keep the array as sorted. This requires 
shifting all the elements after it or creating 
a new array and copy all the elements due to 
the capacity, making the usage of the previous 
data member not valid.

Parameters:
* A pointer to the element to insert.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare the given 
element to insert with any of the array 
elements and returns an std::Compare value.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void insertSortedInt(int value){
	insertSorted(&value,
		compareValue, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.insertSortedInt(2021);
array.insertSortedInt(2020);
/*2020,2021*/
```

## "move" member function:

Moves the data from another std::ds::DArray.
The previous data is deleted.

Parameters:
* A pointer to the DArray to move from.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void moveInt(IntDArray* array){
	move(array, deleteArray);
}

IntDArray first;
first.pushInt(2020);
IntDArray second;
second.pushInt(2021);
first.moveInt(&second);
/*first=2021, second=*/
```

## "pop" member function:

Removes the last element from the array.

Parameters:
* Either nullptr, or a pointer to a construct 
to copy the removed element into.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.

Returns: void.

```
/*In the IntDArray class:*/
int popInt(){
	int value;
	pop(&value, getElement, setElement);
	return value;
}

/*In some function:*/
IntDArray array;
array.pushInt(2020);
array.pushInt(2021);
int value = array.popInt(); /*2021*/
unsigned int size = array.size;
/*1 as 2020.*/
```
	
## "push" member function:

Inserts an element to the array's end. This 
might require creating a new array and copy all 
the elements due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* A pointer to the element to insert.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void pushInt(int value){
	push(&value, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushInt(2020);
unsigned int size = array.size;
/*1 as 2020.*/
array.pushInt(2021);
size = array.size;
/*2 as 2020, 2021.*/
```

## "reserve" member function:

Increases the capacity of the array. This 
requires creating a new array and copy all 
the elements, making the usage of the previous 
data member not valid.

Parameters:
* The new capacity.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void reserveInt(unsigned int newCapacity){
	reserve(newCapacity, getElement, 
		setElement, newArray, deleteArray);
}
	
/*In some function:*/
IntDArray array;
array.reserveInt(2);
unsigned int capacity = array.capacity; /*2*/
unsigned int size = array.size; /*0*/
```

## "reverse" member function:

Reverses the elements of the array.

Parameters:
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a temporary element.

Returns: void.

```
/*In the IntDArray class:*/
void reverseInt(){
	int tmp;
	reverse(getElement, setElement, &tmp);
}

/*In some function:*/
IntDArray array;
array.pushInt(2020);
array.pushInt(2021);
array.reverseInt();
/*2021,2020*/
```

## "set" member function:

Sets the array to be a copy of a subarray.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The array of the subarray to copy.
* The starting index of the subarray to copy 
in its array.
* The size of the subarray to copy.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void setInt(int[] array, 
	unsigned int i, unsigned int elements){
	set((void*)array, i, elements, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.setInt(years, 0, 2);
/*2020,2021*/
```

## "shift" member function:

Shifts rightwise the elements of the array, 
to create an empty space to set manually.
This might require creating a new array and copy 
all the elements due to the capacity, making 
the usage of the previous data member not valid.

Parameters:
* The index in the array to shift from.
* The ammount to shift with.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void(void*, void*)"
function that sets to the given pointed 
element another pointed element.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void shiftInt(unsigned int i, 
	unsigned int elements){
	shift(i, elements, getElement, 
		setElement, newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushInt(2021);
array.shiftInt(0, 1);
(array.getData())[0] = 2020;
/*2020,2021*/
```

## "trim" member function:

Decreases the size of the array.

Parameters:
* The new size.

Returns: void.
	
```
IntDArray array;
array.pushInt(2020);
array.pushInt(2021);
array.trim(1);
size = array.size; /*1 as 2020.*/
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