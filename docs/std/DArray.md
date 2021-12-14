# "std::DArray" class:

Used to create arrays as objects, where the number 
of elements are expected to be changing, thus they
are dynamic arrays.

```
/*To store int values in a dynamic array.*/
class IntDArray : std::DArray {}
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

int[] getData(){
	return (int[])data;
}

/*Some functions to be used by the member functions.*/
static void setElement(
	void* array, unsigned int i, void* element){
	int[] ints = (int[])array;
	ints[i] = *(int*)element;
}
static void* getElement(
	void* array, unsigned int i){
	int[] ints = (int[])array;
	return &ints[i];
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
	
## "erase" member function:

Erases an element from the array. This requires
shifting all the elements after it.

Parameters:
* The index of the element to erase.
* A pointer to a "void(void*, unsigned int, void*)"
function that sets to the given array, at the 
given index, the given pointed element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void eraseInt(unsigned int i){
	erase(i, setElement, getElement,
		newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushBackInt(2020);
array.pushBackInt(2021);
unsigned int size = array.size;
/*2 as 2020, 2021.*/
array.eraseInt(0);
size = array.size; /*1 as 2021.*/
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
* A pointer to a "void(void*, unsigned int, void*)"
function that sets to the given array, at the 
given index, the given pointed element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void insertInt(unsigned int i, int value){
	insert(i, &value, setElement, getElement,
		newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushBackInt(2021);
unsigned int size = array.size;
/*1 as 2021.*/
array.insertInt(0, 2020);
size = array.size;
/*2 as 2020, 2021.*/
```
		
## "popBack" member function:

Removes the last element from the array.

Parameters:
* Either nullptr, or a pointer to a construct 
to copy the removed element into.
* A pointer to a "void(void*, unsigned int, void*)"
function that sets to the given array, at the 
given index, the given pointed element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.

Returns: void.

```
/*In the IntDArray class:*/
int popBackInt(){
	int value;
	popBack(&value, setElement, getElement);
	return value;
}

/*In some function:*/
IntDArray array;
array.pushBackInt(2020);
array.pushBackInt(2021);
int value = array.popBackInt(); /*2021*/
unsigned int size = array.size;
/*1 as 2020.*/
```
	
## "pushBack" member function:

Inserts an element to the array's end. This 
might require creating a new array and copy all 
the elements due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* A pointer to the element to insert.
* A pointer to a "void(void*, unsigned int, void*)"
function that sets to the given array, at the 
given index, the given pointed element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void pushBackInt(int value){
	pushBack(&value, setElement, getElement,
		newArray, deleteArray);
}

/*In some function:*/
IntDArray array;
array.pushBackInt(2020);
unsigned int size = array.size;
/*1 as 2020.*/
array.pushBackInt(2021);
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
* A pointer to a "void(void*, unsigned int, void*)"
function that sets to the given array, at the 
given index, the given pointed element.
* A pointer to a "void*(void*, unsigned int)" 
function that returns a pointer to an element, 
from the given array, at the given index.
* A pointer to a "void*(unsigned int)" function that 
returns a new array, of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array.

Returns: void.

```
/*In the IntDArray class:*/
void reserveInts(unsigned int newCapacity){
	reserve(newCapacity, setElement, getElement,
		newArray, deleteArray);
}
	
/*In some function:*/
IntDArray array;
array.reserveInts(2);
unsigned int capacity = array.capacity; /*2*/
unsigned int size = array.size; /*0*/
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