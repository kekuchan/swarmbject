# "std::ds::CircuralArray" class:

Used to create arrays as objects, where the 
front element can be anywhere in the array, 
with the next elements stored in sequence until 
the end of the array, and then continuing from 
the beginning of the array, until the front 
element. It is useful if only the front and 
back elements are accessed and changed.

```
/*To store int values in a circural array.*/
class IntCircuralArray : 
	std::ds::CircuralArray {

	/*Required, as the CircuralArray does 
		not delete the data automatically, 
		as it does not know its type.*/
	~IntCircuralArray(){
		delete[] (int[])data;
	}
	
	/*Some functions to be used by the member functions.*/
	
	static void deleteArray(void* array){
		delete[] (int[])array;
	}
	
	static void getElement(void* array, 
		unsigned int i, void* value){
		int* year = (int*)value;
		*year = (int[])array[i];
	}
	
	static void* newArray(unsigned int size){
		return (void*)(new int[size]);
	}
	
	static void setElement(void* array, 
		unsigned int i, void* year){
		int[] years = (int[])array;
		years[i] = *(int*)year;
	}
	
	static void setElements(
		void* first, unsigned int i,
		void* second, unsigned int j){
		int[] years = (int[])first;
		years[i] = (int[])second[j];
	}
	
	void pushBack(int value){
		(std::ds::CircuralArray*)this->pushBack(&value, 
			setElements, newArray, deleteArray, setElement);
	}

}
```

## "capacity" data member:

The maximum number of elements that it can 
currently store, thus a new array has to be 
created only when enough elements are inserted so 
that a greater capacity is needed.

```
IntCircuralArray array;
unsigned int capacity = array.capacity; /*0*/
```

## "clear" member function:

Sets the CircuralArray's size to 0.

Returns: void.

```
IntCircuralArray array;
array.pushBack(2021);
array.clear();
unsigned int size = array.getSize(); /*0*/
```
	
## "getBack" member function:

Gets the last element.

Parameters:
* A pointer to a construct to copy the 
element into.
* A pointer to a "void(void*, unsigned int,
void*)" function to copy an element of the 
given array data at the given index to 
the given pointed element.

Returns: void.

```
/*In the IntCircuralArray class:*/
int getBack(){
	int value;
	(std::ds::CircuralArray*)this->getBack(
		&value, getElement);
	return value;
}

/*In some function:*/
IntCircuralArray array;
array.pushBack(2020);
array.pushBack(2021);
int value = array.getBack(); /*2021*/
```

## "getFront" member function:

Gets the first element.

Parameters:
* A pointer to a construct to copy the 
element into.
* A pointer to a "void(void*, unsigned int,
void*)" function to copy an element of the 
given array data at the given index to 
the given pointed element.

Returns: void.

```
/*In the IntCircuralArray class:*/
int getFront(){
	int value;
	(std::ds::CircuralArray*)this->getFront(
		&value, getElement);
	return value;
}

/*In some function:*/
IntCircuralArray array;
array.pushBack(2020);
array.pushBack(2021);
int value = array.getFront(); /*2020*/
```

## "getSize" member function:

Gets the number of elements the array contains.

Returns: unsigned int.

```
IntCircuralArray array;
unsigned int size = array.getSize(); /*0*/
```

## "move" member function:

Moves the data from another std::ds::CircuralArray.
The previous data is deleted.

Parameters:
* A pointer to the CircuralArray to move from.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.

```
/*In the IntCircuralArray class:*/
void move(IntCircuralArray* array){
	(std::ds::CircuralArray*)this->move(
		array, deleteArray);
}

/*In some function:*/
IntCircuralArray first;
first.pushBack(2020);
IntCircuralArray second;
second.pushBack(2021);
first.move(&second);
/*first=2021, second=*/
```

## "popBack" member function:

Gets and removes the last element.

Parameters:
* Either nullptr, or a pointer to a construct 
to copy the removed element into.
* A pointer to a "void(void*, unsigned int,
void*)" function to copy an element of the 
given array data at the given index to 
the given pointed element.

Returns: void.

```
/*In the IntCircuralArray class:*/
int popBack(){
	int value;
	(std::ds::CircuralArray*)this->popBack(
		&value, getElement);
	return value;
}

/*In some function:*/
IntCircuralArray array;
array.pushBack(2020);
array.pushBack(2021);
int value = array.popBack(); /*2021*/
unsigned int size = array.getSize();
/*1 as 2020.*/
```

## "popFront" member function:

Gets and removes the first element.

Parameters:
* Either nullptr, or a pointer to a construct 
to copy the removed element into.
* A pointer to a "void(void*, unsigned int,
void*)" function to copy an element of the 
given array data at the given index to 
the given pointed element.

Returns: void.

```
/*In the IntCircuralArray class:*/
int popFront(){
	int value;
	(std::ds::CircuralArray*)this->popFront(
		&value, getElement);
	return value;
}

/*In some function:*/
IntCircuralArray array;
array.pushBack(2020);
array.pushBack(2021);
int value = array.popFront(); /*2020*/
unsigned int size = array.getSize();
/*1 as 2021.*/
```

## "pushBack" member function:

Inserts an element after the current last 
element, making this the new last element. 
This might require creating a new array and 
copy all the elements due to the capacity.

Parameters:
* A pointer to the element to insert.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
capacity is increased to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*)" function that can set any element of 
the given array data at the given index, 
to be a copy of the given element to insert.

Returns: void.

```
/*In the IntCircuralArray class:*/
void pushBack(int value){
	(std::ds::CircuralArray*)this->pushBack(
		&value, setElements, 
		newArray, deleteArray, setElement);
}

/*In some function:*/
IntCircuralArray array;
array.pushBack(2020);
unsigned int size = array.getSize();
/*1 as 2020.*/
array.pushBack(2021);
size = array.getSize();
/*2 as 2020, 2021.*/
```

## "pushFront" member function:

Inserts a pointer before the current first element,
making this the new first element. This might 
require creating a new array and copy all 
the elements due to the capacity.

* A pointer to the element to insert.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
capacity is increased to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*)" function that can set any element of 
the given array data at the given index, 
to be a copy of the given element to insert.

Returns: void.

```
/*In the IntCircuralArray class:*/
void pushFront(int value){
	(std::ds::CircuralArray*)this->pushFront(
		&value, setElements, 
		newArray, deleteArray, setElement);
}

/*In some function:*/
IntCircuralArray array;
array.pushFront(2021);
unsigned int size = array.getSize();
/*1 as 2021.*/
array.pushFront(2020);
size = array.getSize();
/*2 as 2020, 2021.*/
```

## "reserve" member function:

Increases the capacity of the array. This 
requires creating a new array and copy all 
the elements.

Parameters:
* The new capacity.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
capacity is increased to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.

```
/*In the IntCircuralArray class:*/
void reserve(unsigned int newCapacity){
	(std::ds::CircuralArray*)this->reserve(
		newCapacity, setElements, newArray, deleteArray);
}
	
/*In some function:*/
IntCircuralArray array;
array.reserve(2);
unsigned int capacity = array.capacity; /*2*/
unsigned int size = array.getSize(); /*0*/
```

# Software license

Copyright (c) 2022 SWARMBJECT contributors

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

Copyright (c) 2022 SWARMBJECT contributors

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