# "std::ds::PtrCircuralArray" class:

Used to create pointer containing arrays as 
objects, where the front element can be anywhere 
in the array, with the next elements stored in 
sequence until the end of the array, and then 
continuing from the beginning of the array, 
until the front element. It is useful if only the 
front and back elements are accessed and changed.

## "capacity" data member:

The maximum number of elements that it can 
currently store, thus a new array has to be 
created only when enough elements are inserted so 
that a greater capacity is needed.

```
std::ds::PtrCircuralArray array;
unsigned int capacity = array.capacity; /*0*/
```

## "clear" member function:

Sets the PtrCircuralArray's size to 0. The pointed 
datas are not deleted automatically, as they might be 
still used elsewhere.

Returns: void.

```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2021;
array.pushBack(year);
array.clear();
unsigned int size = array.getSize(); /*0*/
```
	
## "getBack" member function:

Gets the last element.

Returns: void*.
	
```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.getBack()); /*&2021*/
```

## "getFront" member function:

Gets the first element.
	
Returns: void*.
	
```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.getFront()); /*&2020*/
```

## "getSize" member function:

Gets the number of pointers the array contains.

Returns: unsigned int.

```
std::ds::PtrCircuralArray array;
unsigned int size = array.getSize(); /*0*/
```

## "move" member function:

Moves the data from another std::ds::PtrCircuralArray.
The previous data is deleted, however the 
pointed data is not deleted automatically, 
as it might be still used elsewhere.

Parameters:
* A pointer to the PtrCircuralArray to move from.

Returns: void.

```
std::ds::PtrCircuralArray first;
int* year = new int;
*year = 2020;
first.pushBack(year);
std::ds::PtrCircuralArray second;
year = new int;
*year = 2021;
second.pushBack(year);
delete first.getBack();
first.move(&second);
/*first=&2021, second=*/
```

## "popBack" member function:

Gets and removes the last element.
	
Returns: void*.

```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.popBack()); /*&2021*/
unsigned int size = array.getSize();
/*1 as &2020*/
```

## "popFront" member function:

Gets and removes the first element.
	
Returns: void*.

```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
year = (int*)(array.popFront()); /*&2020*/
unsigned int size = array.getSize();
/*1 as &2021*/
```

## "pushBack" member function:

Inserts a pointer after the current last element,
making this the new last element. This might 
require creating a new array and copy all 
the elements due to the capacity.

Parameters:
* The pointer to insert.

Returns: void.

```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2020;
array.pushBack(year);
year = new int;
*year = 2021;
array.pushBack(year);
/*&2020,&2021*/
```

## "pushFront" member function:

Inserts a pointer before the current first element,
making this the new first element. This might 
require creating a new array and copy all 
the elements due to the capacity.

Parameters:
* The pointer to insert.

Returns: void.

```
std::ds::PtrCircuralArray array;
int* year = new int;
*year = 2021;
array.pushFront(year);
year = new int;
*year = 2020;
array.pushFront(year);
/*&2020,&2021*/
```

## "reserve" member function:

Increases the capacity of the array. This 
requires creating a new array and copy all 
the elements.

Parameters:
* The new capacity.

Returns: void.

```
std::ds::PtrCircuralArray array;
array.reserve(2);
unsigned int capacity = array.capacity; /*2*/
unsigned int size = array.getSize(); /*0*/
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