# "std::PtrDArray" class:

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
std::PtrDArray array;
unsigned int capacity = array.capacity; /*0*/
```

## "data" data member:

The contained array of pointers. It is a 
void*[], as the PtrDArray does not know the 
actual pointer type, thus it has to be converted.

```
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
int*[] years = (int*[])(array.data);
/*&2020,&2021*/
```

## "size" data member:

The number of elements in the array as 
an unsigned int.

```
std::PtrDArray array;
unsigned int size = array.size; /*0*/
```

## "clear" member function:

Sets the PtrDArray's size to 0. The pointed datas 
are not deleted automatically, as they might be 
still used elsewhere.

Returns: void.

```
std::PtrDArray array;
int* year = new int;
*year = 2021;
array.pushBack(year);
array.clear();
unsigned int size = array.size; /*0*/
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
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
/*When not needed anymore:*/
delete (int*)(array.data[0]);
array.erase(0, 1);
/*&2021*/
```

## "find" member function:

Finds the first occurence of an element.

Parameters:
* A pointer to an element to find.
* A pointer to a "char(void*,void*)" function that 
can compare the given element to find with any of 
the array elements and returns 0 if equals,
and a non 0 char otherwise.

Returns: either nullptr, or an element of the 
array as void* if found.

```
char compare(void* find, void* element){
	if (*(int*)find == *(int*)element)){
		return 0;
	} else {
		return 1;
	}
}

/*In some function:*/
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
int find = 2021;
int* year = (int*)(array.find(
	&find, compare)); /*array.data[1]*/
```

## "findSorted" member function:

Finds an element, if the array is sorted.

Parameters:
* A pointer to an element to find.
* A pointer to a "char(void*,void*)" function that 
can compare the given element to find with any of 
the array elements and returns a positive char if 
its first parameter is greater than the second, 
0 if equals, and a negative char otherwise.

Returns: either nullptr, or an element of the 
array as void* if found.

```
char compare(void* find, void* element){
	if (*(int*)find == *(int*)element)){
		return 0;
	} else {
		return 1;
	}
}

/*In some function:*/
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
int find = 2021;
int* year = (int*)(array.findSorted(
	&find, compare)); /*array.data[1]*/
```

## "getBack" member function:

Gets the last element.
	
Returns: void*.

```
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.getBack()); /*&2021*/
```

## "indexOfSortedNew" member function:

Finds an element, if the array is sorted.

Parameters:
* A pointer to an element to find.
* A pointer to a "char(void*,void*)" function that 
can compare the given element to find with any of 
the array elements and returns a positive char if 
its first parameter is greater than the second, 
0 if equals, and a negative char otherwise.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
char compare(void* insert, void* element){
	return std::Memory::compareInt(
		*(int*)insert, *(int*)element);
}
		
/*In some function:*/
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
int find = 2021;
unsigned int i = array.indexOfSortedNew(
	&find, compare)); /*2*/
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
std::PtrDArray array;
int* year = new int;
*year = 2021;
array.pushBack(year);
year = new int;
*year = 2020;
array.insert(0, year, 1);
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
* A pointer to a "char(void*,void*)" function that 
can compare the given element to insert with any of 
the array elements and returns a positive char if 
its first parameter is greater than the second, 
0 if equals, and a negative char otherwise.

Returns: void.

```
char compare(void* insert, void* element){
	return std::Memory::compareInt(
		*(int*)insert, *(int*)element);
}
		
/*In some function:*/
std::PtrDArray array;
int* year = new int;
*year = 2021;
array.insertSorted(year, compare);
year = new int;
*year = 2020;
array.insertSorted(year, compare);
/*&2020,&2021*/
```

## "popBack" member function:

Gets and removes the last element.
	
Returns: void*.

```
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.popBack()); /*&2021*/
unsigned int size = array.size;
/*1 as &2020*/
```

## "pushBack" member function:

Inserts an element to the array's end. This 
might require creating a new array and copy all 
the elements due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The pointer to insert.

Returns: void.

```
std::PtrDArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
/*&2020,&2021*/
```

## "reserve" member function:

Increases the capacity of the array. This 
requires creating a new array and copy all 
the elements, making the usage of the previous 
data member not valid.

Parameters:
* The new capacity.

Returns: void.

```
std::PtrDArray array;
array.reserve(2);
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