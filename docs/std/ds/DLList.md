# "std::ds::DLList" class:

Used for objects as part of a doubly linked list.
Each object in the list has a pointer to the next 
and the previous element in the list.

```
/*In Year.scf*/
class Year {
	int value;
	std::ds::DLList list;
	
	/*Used by the member functions.*/
	
	static std::ds::DLList* getList(void* year){
		return &((Year*)year->list);
	}
	
	static unsigned char compare(
		void* element, void* year){
		return std::val::Int::compare(
			(Year*)element->value,
			(Year*)year->value);
	}
	
	static unsigned char compareValue(
		void* year, void* i){
		return std::val::Int::compare(
			(Year*)year->value, *(int*)i);
	}
}
```

## "next" data member:

Points to the next element 
in the list, as a void*.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2020.*/
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
year = (Year*)(front->list.next); /*2021*/
```

## "previous" data member:

Points to the previous element 
in the list, as a void*.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2020.*/
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
year = (Year*)(back->list.previous); /*2020*/
```

## "erase" member function:

Removes the element from the list. The 
element is not deleted automatically, 
as it might be still used elsewhere.

Parameters:
* Either nullptr or a pointer to a 
construct, that points to the front element.
* Either nullptr or a pointer to a 
construct, that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*When not needed anymore:*/
year = front;
front->list.erase(&front,
	&back, Year::getList);
delete year;
/*front=2020,back=2020.*/
```

## "getSize" static function:

Gets the number of elements the list contains.
This requires iterating through all the 
elements with the next pointer.

Parameters:
* A pointer to the front element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: unsigned int.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
unsigned int size =
	std::ds::DLList::getSize(front, Year::getList);
/*2 as 2020,2021.*/
```

## "getSizeBack" static function:

Gets the number of elements the list contains.
This requires iterating through all the 
elements with the previous pointer.

Parameters:
* A pointer to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: unsigned int.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
unsigned int size =
	std::ds::DLList::getSizeBack(
		back, Year::getList);
/*2 as 2020,2021.*/
```

## "insert" static function:

Returns where an element as the next element 
could be inserted, if the list is sorted. This 
requires iterating through the elements with 
the next pointer, until the position is found.

Parameters:
* A pointer to the element to insert.
* A pointer to the front element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the list 
elements with the given element to insert 
and returns an std::Compare value.

Returns: the previous element.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
int i = 2021;
year = std::ds::DLList::insert(&i, front,
	Year::getList, Year::compareValue);
/*2020*/
```

## "insertBack" static function:

Returns where an element as the next element 
could be inserted, if the list is sorted. This 
requires iterating through the elements with 
the previous pointer, until the position is found.

Parameters:
* A pointer to the element to insert.
* A pointer to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the list 
elements with the given element to insert 
and returns an std::Compare value.

Returns: the previous element.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
int i = 2021;
year = std::ds::DLList::insertBack(&i, back, 
	Year::getList, Year::compareValue);
/*2020*/
```

## "insertNext" static function:

Inserts an element as the next element. If the 
element is already part of the list, then it 
must be removed before calling this function.

Parameters:
* A pointer to the previous element.
* A pointer to the element to insert.
* Either nullptr or a pointer to a 
construct, that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::insertNext(
	front, year, &back, Year::getList);
/*front=2020,back=2021.*/
```

## "insertSorted" member function:

Inserts an element to the list at a position 
to keep the list as sorted. This requires 
iterating through the elements, until the 
position is found. If the element is already 
part of the list, then it must be removed 
before calling this function.

Parameters:
* A pointer to the element to insert.
* Either nullptr but only if the next 
parameter is not nullptr, or a pointer to a 
construct, that points to the front element.
* Either nullptr but only if the previous 
parameter is not nullptr, or a pointer to a 
construct, that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the list 
elements with the given element to insert 
and returns an std::Compare value.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2021;
std::ds::DLList::insertSorted(year, &front,
	&back, Year::getList, Year::compare);
/*front=2021,back=2021.*/
year = new Year;
year->value = 2020;
std::ds::DLList::insertSorted(year, &front,
	&back, Year::getList, Year::compare);
/*front=2020,back=2021.*/
```

## "popBack" static function:

Removes the last element from the list. The 
element is not deleted automatically, as it 
might be still used elsewhere.

Parameters:
* Either nullptr or a pointer to a 
construct, that points to the front element.
* A pointer to a construct, that points to 
the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
/*When not needed anymore:*/
std::ds::DLList::popBack(&front,
	&back, Year::getList);
delete year;
/*front=2020,back=2020.*/
```

## "popFront" static function:

Removes the first element from the list. The 
element is not deleted automatically, as it 
might be still used elsewhere.

Parameters:
* A pointer to a construct, that points to 
the front element.
* Either nullptr or a pointer to a 
construct, that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
/*When not needed anymore:*/
year = front;
std::ds::DLList::popFront(&front,
	&back, Year::getList);
delete year;
/*front=2021,back=2021.*/
```

## "pushBack" static function:

Inserts an element after the current last element, 
making this the new last element. If the element is 
already part of the list, then it must be removed 
before calling this function.

Parameters:
* A pointer to the element to insert.
* Either nullptr or a pointer to a 
construct, that points to the front element.
* Either nullptr to iterate through the list from 
the front element or a pointer to a construct, 
that points directly to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2020.*/
year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
```

## "pushFront" static function:

Inserts an element before the current first element, 
making this the new first element. If the element 
is already part of the list, then it must be 
removed before calling this function.

Parameters:
* A pointer to the element to insert.
* Either nullptr to iterate through the list from 
the back element or a pointer to a construct, 
that points directly to the front element.
* Either nullptr or a pointer to a construct, 
that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2021;
std::ds::DLList::pushFront(year, &front,
	&back, Year::getList);
/*front=2021,back=2021.*/
year = new Year;
year->value = 2020;
std::ds::DLList::pushFront(year, &front,
	&back, Year::getList);
/*front=2020,back=2021.*/
```

## "sort" static function:

Sorts the elements the list contains.

Parameters:
* Either nullptr but only if the next 
parameter is not nullptr, or a pointer to a 
construct, that points to the front element.
* Either nullptr but only if the previous 
parameter is not nullptr, or a pointer to a 
construct, that points to the back element.
* A pointer to an "std::ds::DLList*(void*)" 
function that returns a pointer to the 
std::ds::DLList data member of the given element.
* A pointer to an "unsigned char(void*,void*)" 
function that can compare any of the list 
elements and returns an std::Compare value.

Returns: void.

```
Year* front = nullptr;
Year* back = nullptr;
Year* year = new Year;
year->value = 2021;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2021,back=2021.*/
year = new Year;
year->value = 2020;
std::ds::DLList::pushBack(year, &front,
	&back, Year::getList);
/*front=2021,back=2020.*/
std::ds::DLList::sort(&front, &back, 
	Year::getList, Year::compare);
/*front=2020,back=2021.*/
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