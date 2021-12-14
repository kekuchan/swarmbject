# "std::PtrArray" class:

Used to create pointer containing arrays as 
objects, where the number of elements are 
not expected to be changing.

## "data" data member:

The contained array of pointers. It is a 
void*[], as the PtrArray does not know the 
actual pointer type, thus it has to be converted.
	
```
std::PtrArray array;
array.setSize(2);
int*[] years = (int*[])(array.data);
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
/*&2020,&2021*/
```

## "size" data member:

The number of elements in the array as 
an unsigned int.

```
std::PtrArray array;
unsigned int size = array.size; /*0*/
```

## "erase" member function:

Erases elements from the array. As it creates a 
new array and copy the remaining elements, usage of 
the previous data member is not valid. The pointed 
data is not deleted automatically, as it might be 
still used elsewhere.

Parameters:
* The index of the first element to erase.
* The number of elements to erase.

Returns: void.

```
std::PtrArray array;
array.setSize(2);
int*[] years = (int*[])(array.data);
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
/*When not needed anymore:*/
delete years[0];
array.erase(0, 1);
/*&2021*/
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
	return std::Memory::compareInt(
		*(int*)find, *(int*)element);
}

/*In some function:*/
std::PtrArray array;
array.setSize(2);
int*[] years = (int*[])(array.data);
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
int find = 2021;
int* year = (int*)(array.findSorted(
	&find, compare)); /*years[1]*/
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
char compare(void* find, void* element){
	return std::Memory::compareInt(
		*(int*)find, *(int*)element);
}

/*In some function:*/
std::PtrArray array;
array.setSize(2);
int*[] years = (int*[])(array.data);
years[0] = new int;
*years[0] = 2020;
years[1] = new int;
*years[1] = 2021;
int find = 2021;
unsigned int i = array.indexOfSortedNew(
	&find, compare)); /*2*/
```

## "insert" member function:

Inserts an element to the array. As it creates 
a new array and copy all the elements, usage of 
the previous data member is not valid.

Parameters:
* The index in the array to insert at.
* A pointer to insert.
* The number of times to insert the element.

Returns: void.

```
std::PtrArray array;
int* year = new int;
*year = 2021;
array.insert(0, year, 1);
year = new int;
*year = 2020;
array.insert(0, year, 1);
/*&2020,&2021*/
```

## "insertSorted" member function:

Inserts an element to the array at a position to 
keep the array as sorted. As it creates a new array 
and copy all the elements, usage of the previous 
data member is not valid.

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
std::PtrArray array;
int* year = new int;
*year = 2021;
array.insertSorted(year, compare);
year = new int;
*year = 2020;
array.insertSorted(year, compare);
/*&2020,&2021*/
```

## "setSize" member function:

Changes the size of the array. As it creates 
a new array and copy all the elements, usage of 
the previous data member is not valid.

Parameters:
* The new size the array.

Returns: void.

```
std::PtrArray array;
array.setSize(1);
unsigned int size = array.size; /*1*/
array.setSize(2);
size = array.size; /*2*/
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