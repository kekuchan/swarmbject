# "std::ds::BalBinTree" class:

Used for objects as part of a binary tree, that 
is balanced, to have the minimum ammount of levels.

```
/*In Year.scf*/
class Year {
	int value;
	std::ds::BinTree tree;
	
	/*Used by the member functions.*/
	
	static std::ds::BinTree* getTree(void* year){
		return &(Year*)year->tree;
	}
	
	static unsigned char compare(
		void* first, void* second){
		return std::arr::Int::compareValue(
			(Year*)first->value,
			(Year*)second->value);
	}
	
	static unsigned char compareValue(
		void* year, void* i){
		return std::arr::Int::compareValue(
			(Year*)year->value, *(int*)i);
	}
	
	static void erase(void* year){
		delete (Year*)year;
	}
	
	static void* getElement(void* array, 
		unsigned int i){
		Year* year = new Year;
		year->value = (int[])array[i];
		return year;
	}
	
}
```

## "root" data member:

The root element of the tree, as a void*.

```
std::ds::BalBinTree tree;
Year* year = (Year*)(tree.root); /*nullptr*/
```

## "size" data member:

The number of elements in the tree as 
an unsigned int.

```
std::ds::BalBinTree tree;
unsigned int size = tree.size; /*0*/
```

## "clear" member function:

Removes all the elements from the tree. 
The elements are not deleted automatically, 
as they might be still used elsewhere.

Parameters:
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.
* A pointer to a "void(void*)" function 
that is called with each removed element.

Returns: void.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
tree.clear(Year::getTree,
	Year::erase);
unsigned int size = tree.size; /*0*/
```

## "create" member function:

Creates a tree, from some construct. If the 
tree is not empty, its elements are not removed 
automatically, as they might be still used elsewhere.

Parameters:
* A pointer to some construct.
* The starting index of the construct.
* The size of the construct.
* A pointer to a "void*(void*, unsigned int)" 
function that returns an element from the 
given construct at the given index.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.

Returns: void.

```
int[] years = new int[2];
years[0] = 2021;
years[1] = 2022;
std::ds::BalBinTree tree;
tree.create(
	years, 0, 2, 
	Year::getElement, Year::getTree);
```

## "erase" member function:

Removes an element from the tree. The element 
is not deleted automatically, as it might be 
still used elsewhere.

Parameters:
* The element to remove.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.

Returns: void.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2021;
tree.insert(year, 
	Year::getTree, Year::compare);
year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
tree.erase(year, Year::getTree);
/*root=2022*/
```

## "find" member function:

Finds an element in the tree.

* A pointer to an element to find.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.
* A pointer to an "unsigned char(void*, void*)" 
function that can compare any element of the 
tree, with the given element to find, 
and returns an std::Compare value.

Returns: nullptr if not found, 
otherwise the element.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
int i = 2022;
year = (Year*)(tree.find(&i, 
	Year::getTree, Year::compareValue));
```

## "first" member function:

Gets the first element in the tree, as a void*.

Parameters:
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.

Returns: void*.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2021;
tree.insert(year, 
	Year::getTree, Year::compare);
year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
year = (Year*)(tree.first(
	Year::getTree)); /*2021*/
```

## "insert" member function:

Inserts an element to the tree.

* A pointer to the element to insert.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.
* A pointer to an "unsigned char(void*, void*)" 
function that can compare any element of the 
tree, with the given element to insert,
and returns an std::Compare value.

Returns: void.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
/*root=2022*/
```

## "last" static function:
		
Gets the last element in the tree, as a void*.

Parameters:
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.

Returns: void*.

```
Year* year = new Year;
year->value = 2021;
tree.insert(year, 
	Year::getTree, Year::compare);
year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
year = (Year*)(tree.last(
	Year::getTree)); /*2022*/
```

## "max" member function:

Finds an element, or if not found, then 
its logically previous element in the tree.

* A pointer to an element to find.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.
* A pointer to an "unsigned char(void*, void*)" 
function that can compare any element of the 
tree, with the given element to find, 
and returns an std::Compare value.

Returns: void*.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2021;
tree.insert(year, 
	Year::getTree, Year::compare);
int i = 2022;
year = (Year*)(tree.max(&i, 
	Year::getTree, Year::compareValue)); /*2021*/
```

## "min" member function:

Finds an element, or if not found, then 
its logically next element in the tree.

* A pointer to an element to find.
* A pointer to an "std::ds::BinTree*(void*)" function 
that returns a pointer to the std::ds::BinTree data 
member of the given element.
* A pointer to an "unsigned char(void*, void*)" 
function that can compare any element of the 
tree, with the given element to find, 
and returns an std::Compare value.

Returns: void*.

```
std::ds::BalBinTree tree;
Year* year = new Year;
year->value = 2022;
tree.insert(year, 
	Year::getTree, Year::compare);
int i = 2021;
year = (Year*)(tree.min(&i, 
	Year::getTree, Year::compareValue)); /*2022*/
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