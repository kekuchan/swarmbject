# "std::ds::Array" class:

Used to create arrays as objects, where the 
number of elements are not expected to be changing.

```
/*To store int values in an array.*/
class IntArray : std::ds::Array {

	/*Required, as the Array does not delete the 
		data automatically, as it does not know its type.*/
	~IntArray(){
		delete[] (int[])data;
	}
	
	/*Some functions to be used by the member functions.*/
	
	static unsigned char compareElement(
		void* years, unsigned int i, void* year){
		return std::val::Int::compare(
			(int[])years[i], *(int*)year);
	}
	
	static unsigned char compareElements(
		void* first, unsigned int i,
		void* second, unsigned int j){
		return std::val::Int::compare(
			(int[])first[i], (int[])second[j]);
	}
	
	static void deleteArray(void* array){
		delete[] (int[])array;
	}
	
	static void getElement(void* array, 
		unsigned int i, void* value){
		int* year = (int*)value;
		*year = (int[])array[i];
	}
	
	static unsigned char equal(
		void* first, unsigned int i,
		void* second, unsigned int j){
		if ((int[])first[i] == (int[])second[j])
			{return std::Compare::equal;}
		return std::Compare::unset;
	}
	
	static unsigned char equalElement(
		void* years, unsigned int i, void* year){
		if ((int[])years[i] == *(int*)year)
			{return std::Compare::equal;}
		return std::Compare::unset;
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
	
	static void switchElements(
		void* array, unsigned int i,
		unsigned int j){
		int[] years = (int[])array;
		int year = years[i];
		years[i] = years[j];
		years[j] = year;
	}
	
	int[] create(unsigned int elements){
		return (int[])((std::ds::Array*)this->create(
			elements, newArray, deleteArray));
	}

}
```

## "data" data member:

The contained array of data. It is a void*, as 
the Array does not know its actual type, thus 
it has to be converted.

```
/*In the IntArray class:*/
int[] getData(){
	return (int[])data;
}
```
	
## "size" data member:

The number of elements in the array as 
an unsigned int.

```
IntArray array;
unsigned int size = array.size; /*0*/
```

## "add" member function:

Inserts an element to the array's end. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* A pointer to the element to insert.
* The number of times to insert the element.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
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
/*In the IntArray class:*/
void add(int value, 
	unsigned int elements){
	(std::ds::Array*)this->add(
		&value, elements, setElements, newArray, 
		deleteArray, setElement);
}

/*In some function:*/
IntArray array;
array.add(2021, 2);
/*2021,2021*/
```

## "addRange" member function:

Inserts a subarray to the array's end. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* The array of the subarray to insert.
* The starting index of the subarray to insert 
in its array.
* The size of the subarray to insert.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*, unsigned int)" function that can set 
any element of the given array data at the 
given index, to be a copy of an element of the 
given subarray at the given index to insert.

Returns: void.

```
/*In the IntArray class:*/
void addRange(int[] array, 
	unsigned int i, unsigned int elements){
	(std::ds::Array*)this->addRange(
		(void*)array, i, elements, setElements, 
		newArray, deleteArray, setElements);
}

/*In some function:*/
IntArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.addRange(years, 0, 2);
/*2020,2021*/
```

## "clear" member function:

Clears the array to its initial state. As 
it deletes the contained array, usage of 
the previous data member is not valid.

Parameters:
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.

```
/*In the IntArray class:*/
void clear(){
	(std::ds::Array*)this->clear(deleteArray);
}

/*In some function:*/
IntArray array;
array.create(1);
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
* A pointer to an "unsigned char(void*, unsigned int, 
void*, unsigned int)" function that can compare 
any element of the given array data at the given 
index, with any element of the given subarray at 
the given index, and returns an std::Compare value.

Returns: an std::Compare value.

```
/*In the IntArray class:*/
unsigned char compare(int[] array, 
	unsigned int i, unsigned int elements){
	return (std::ds::Array*)this->compare(
		(void*)array, i, elements, compareElements);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2020;
years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.compare(years, 0, 2);
/*std::Compare::greater as 
	2021,2020 > 2020,2021.*/
```

## "copy" member function:

Copy an element to the array, by 
replacing the values.

Parameters:
* The starting index in the array to copy to.
* A pointer to the element to copy.
* The number of times to copy the element.
* A pointer to an "void(void*, unsigned int, 
void*)" function that can set any element of 
the given array data at the given index, 
to be a copy of the given element.

Returns: void.

```
/*In the IntArray class:*/
void copy(unsigned int start, 
	int value, unsigned int elements){
	(std::ds::Array*)this->copy(
		start, &value, elements, setElement);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2020;
array.copy(0, 2021, 2);
/*2021,2021*/
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
* A pointer to an "void(void*, unsigned int, 
void*, unsigned int)" function that can set 
any element of the given array data at the 
given index, to be a copy of an element of the 
given subarray at the given index to insert.

Returns: void.

```
/*In the IntArray class:*/
void copyRange(unsigned int start, int[] array, 
	unsigned int i, unsigned int elements){
	(std::ds::Array*)this->copyRange(
		start, (void*)array, i, elements, setElements);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2020;
years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.copyRange(0, years, 0, 2);
/*2020,2021*/
```

## "create" member function:

Sets the array with empty space to set manually. 
This might require creating a new array, making 
the usage of the previous data member not valid.

Parameters:
* The size of the array to create.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: the array data as void*.

```
/*In the IntArray class:*/
int[] create(unsigned int elements){
	return (int[])((std::ds::Array*)this->create(
		elements, newArray, deleteArray));
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
/*2020,2021*/
```

## "erase" member function:

Erases elements from the array. As it creates 
a new array and copy the remaining elements, 
usage of the previous data member is not valid. 

Parameters:
* The index of the first element to erase.
* The number of elements to erase.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.

```
/*In the IntArray class:*/
void erase(unsigned int i, 
	unsigned int elements){
	(std::ds::Array*)this->erase(i, elements, 
		setElements, newArray, deleteArray);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
unsigned int size = array.size;
/*2 as 2020, 2021.*/
array.erase(0, 1);
size = array.size; /*1 as 2021.*/
```

## "find" static function:

Finds the first occurence of an element.

Parameters:
* A pointer to an element to find.
* A pointer to an "unsigned char(void*, 
unsigned int, void*)" function that can compare 
any element of the given array data at the given 
index, with the given element to find, and 
returns std::Compare::equal if equal, or 
something else otherwise.
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntArray class:*/
unsigned int find(
	unsigned int element, unsigned int i){
	return (std::ds::Array*)this->find(
		&element, equalElement, i);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2021;
unsigned int i = array.find(
	2021, 0); /*1*/
```

## "findLast" static function:

Finds the first occurence of an element,
but starting backwards in the array.

Parameters:
* A pointer to an element to find.
* A pointer to an "unsigned char(void*, 
unsigned int, void*)" function that can compare 
any element of the given array data at the given 
index, with the given element to find, and 
returns std::Compare::equal if equal, or 
something else otherwise.
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntArray class:*/
unsigned int findLast(
	unsigned int element, unsigned int i){
	return (std::ds::Array*)this->findLast(
		&element, equalElement, i);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2021;
unsigned int i = array.findLast(
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
* A pointer to an "unsigned char(void*, unsigned int, 
void*, unsigned int)" function that can compare 
any element of the given array data at the 
given index, with any element of the given 
subarray at the given index to find, and 
returns std::Compare::equal if equal, or 
something else otherwise.
* The index + 1 position to 
search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
/*In the IntArray class:*/
unsigned int findLastRange(
	int[] array, unsigned int i, 
	unsigned int elements, unsigned int start){
	return (std::ds::Array*)this->findLastRange(
		(void*)array, i, elements, equal, start);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2021;
unsigned int i = array.findLastRange(
	years, 0, 1, array.size); /*2*/
```

## "findRange" static function:

Finds the first occurence of a subarray 
in the array.

Parameters:
* The array of the subarray to find.
* The starting index of the subarray to find 
in its array.
* The size of the subarray to find.
* A pointer to an "unsigned char(void*, unsigned int, 
void*, unsigned int)" function that can compare 
any element of the given array data at the 
given index, with any element of the given 
subarray at the given index to find, and 
returns std::Compare::equal if equal, or 
something else otherwise.
* The starting index to search from in the array.

Returns: 0, if not found, otherwise the 
index + 1 position of the starting element.

```
/*In the IntArray class:*/
unsigned int findRange(
	int[] array, unsigned int i, 
	unsigned int elements, unsigned int start){
	return (std::ds::Array*)this->findRange(
		(void*)array, i, elements, equal, start);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2021;
years[1] = 2021;
unsigned int i = array.findRange(
	years, 0, 1, 0); /*1*/
```

## "findSorted" member function:

Finds an element, if the array is sorted.

Parameters:
* A pointer to an element to find.
* A pointer to an "unsigned char(void*, 
unsigned int, void*)" function that can compare 
any element of the given array data at the given 
index, with the given element to find, and 
returns an std::Compare value.

Returns: 0, if not found, otherwise the 
index + 1 position of the element.

```
/*In the IntArray class:*/
unsigned int findSorted(
	unsigned int element){
	return (std::ds::Array*)this->findSorted(
		&element, compareElement);
}
		
/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
unsigned int i = 
	array.findSorted(2021); /*2*/
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
/*In the IntArray class:*/
int getBack(){
	int value;
	(std::ds::Array*)this->getBack(
		&value, getElement);
	return value;
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
int value = array.getBack(); /*2021*/
```

## "grow" member function:

Grows the array, with empty space to set manually.
As it creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* The ammount to grow with.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: the array data as void*.

```
/*In the IntArray class:*/
int[] grow(unsigned int elements){
	return (int[])((std::ds::Array*)this->grow(
		elements, setElements, newArray, deleteArray));
}

/*In some function:*/
IntArray array;
int[] years = array.create(1);
years[0] = 2020;
years = array.grow(1);
years[1] = 2021;
/*2020,2021*/
```

## "insert" member function:
		
Inserts an element to the array. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* The index in the array to insert at.
* A pointer to the element to insert.
* The number of times to insert the element.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
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
/*In the IntArray class:*/
void insert(unsigned int i, int value, 
	unsigned int elements){
	(std::ds::Array*)this->insert(
		i, &value, elements, setElements, newArray, 
		deleteArray, setElement);
}

/*In some function:*/
IntArray array;
int[] years = array.create(1);
years[0] = 2021;
unsigned int size = array.size;
/*1 as 2021.*/
array.insert(0, 2020, 1);
size = array.size;
/*2 as 2020, 2021.*/
```
	
## "insertRange" member function:

Inserts a subarray to the array. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* The index in the array to insert at.
* The array of the subarray to insert.
* The starting index of the subarray to insert 
in its array.
* The size of the subarray to insert.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*, unsigned int)" function that can set 
any element of the given array data at the 
given index, to be a copy of an element of the 
given subarray at the given index to insert.

Returns: void.

```
/*In the IntArray class:*/
void insertRange(
	unsigned int start, int[] array, 
	unsigned int i, unsigned int elements){
	(std::ds::Array*)this->insertRange(
		start, (void*)array, i, elements, setElements, 
		newArray, deleteArray, setElements);
}

/*In some function:*/
IntArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.insertRange(0, years, 0, 2);
/*2020,2021*/
```

## "insertSorted" member function:

Inserts an element to the array at a position 
to keep the array as sorted. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* A pointer to the element to insert.
* A pointer to an "unsigned char(void*, 
unsigned int, void*) " function that can 
compare any element of the given array data 
at the given index, with the given element 
to insert, and returns an std::Compare value.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
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
/*In the IntArray class:*/
void insertSorted(int value){
	(std::ds::Array*)this->insertSorted(
		&value, compareElement, setElements, 
		newArray, deleteArray, setElement);
}

/*In some function:*/
IntArray array;
array.insertSorted(2021);
array.insertSorted(2020);
/*2020,2021*/
```

## "move" member function:

Moves the data from another std::ds::Array.
The previous data is deleted.

Parameters:
* A pointer to the Array to move from.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.

```
/*In the IntArray class:*/
void move(IntArray* array){
	(std::ds::Array*)this->move(
		array, deleteArray);
}

IntArray first;
int[] years = first.create(1);
years[0] = 2020;
IntArray second;
years = second.create(1);
years[0] = 2021;
first.move(&second);
/*first=2021, second=*/
```

## "pop" member function:

Removes the last element from the array. As it 
creates a new array and copy the remaining elements, 
usage of the previous data member is not valid. 

Parameters:
* Either nullptr, or a pointer to a construct 
to copy the removed element into.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to a "void(void*, unsigned int,
void*)" function to copy an element of the 
given array data at the given index to 
the given pointed element.

Returns: void.

```
/*In the IntArray class:*/
int pop(){
	int value;
	(std::ds::Array*)this->pop(
		&value, setElements, 
		newArray, deleteArray, getElement);
	return value;
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
int value = array.pop(); /*2021*/
unsigned int size = array.size;
/*1 as 2020.*/
```

## "push" member function:

Inserts an element to the array's end. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* A pointer to the element to insert.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
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
/*In the IntArray class:*/
void push(int value){
	(std::ds::Array*)this->push(&value, setElements, 
		newArray, deleteArray, setElement);
}

/*In some function:*/
IntArray array;
array.push(2020);
unsigned int size = array.size;
/*1 as 2020.*/
array.push(2021);
size = array.size;
/*2 as 2020, 2021.*/
```

## "reverse" member function:

Reverses the elements of the array.

Parameters:
* A pointer to a "void(void*, unsigned int, 
unsigned int)" function that switch the value 
of any element of the given array data at the 
given index, with another at a given index.

Returns: void.

```
/*In the IntArray class:*/
void reverse(){
	(std::ds::Array*)this->reverse(
		switchElements);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
array.reverse();
/*2021,2020*/
```

## "set" member function:

Sets the array to be a copy of an element.
This might require creating a new array, making 
the usage of the previous data member not valid.

Parameters:
* A pointer to the element to copy.
* The number of times to copy the element.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*)" function that can set any element of 
the given array data at the given index, 
to be a copy of the given element.

Returns: void.

```
/*In the IntArray class:*/
void set(int value, unsigned int elements){
	(std::ds::Array*)this->set(
		&value, elements, newArray, 
		deleteArray, setElement);
}

/*In some function:*/
IntArray array;
array.set(2021, 2);
/*2021,2021*/
```

## "setRange" member function:

Sets the array to be a copy of a subarray.
This might require creating a new array, making 
the usage of the previous data member not valid.

Parameters:

* The array of the subarray to copy.
* The starting index of the subarray to copy 
in its array.
* The size of the subarray to copy.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.
* A pointer to an "void(void*, unsigned int, 
void*, unsigned int)" function that can set 
any element of the given array data at the 
given index, to be a copy of an element of the 
given subarray at the given index.

Returns: void.

```
/*In the IntArray class:*/
void setRange(int[] array, 
	unsigned int i, unsigned int elements){
	(std::ds::Array*)this->setRange((void*)array, 
		i, elements, newArray, deleteArray, setElements);
}

/*In some function:*/
IntArray array;
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
array.setRange(years, 0, 2);
/*2020,2021*/
```

## "shift" member function:

Shifts rightwise the elements of the array, to 
create an empty space to set manually. As it 
creates a new array and copy all the elements, 
usage of the previous data member is not valid. 

Parameters:
* The index in the array to shift from.
* The ammount to shift with.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: the array data as void*.

```
/*In the IntArray class:*/
int[] shift(unsigned int i, 
	unsigned int elements){
	return (int[])((std::ds::Array*)this->shift(i, 
		elements, setElements, newArray, deleteArray));
}

/*In some function:*/
IntArray array;
int[] years = array.create(1);
years[0] = 2021;
years = array.shift(0, 1);
years[0] = 2020;
/*2020,2021*/
```

## "trim" member function:

Decreases the size of the array. As it creates 
a new array and copy the remaining elements, 
usage of the previous data member is not valid. 

Parameters:
* The new size.
* A pointer to a "void(void*, unsigned int, 
void*, unsigned int)" function used when the 
new array is created to set any element of 
the given new array data at the given index, 
to be a copy of an element of the given 
previous array data at the given index.
* A pointer to a "void*(unsigned int)" function 
that returns a new array data of the given size.
* A pointer to a "void(void*)" function that 
deletes the given array data.

Returns: void.
	
```
/*In the IntArray class:*/
void trim(unsigned int elements){
	(std::ds::Array*)this->trim(
		elements, setElements, newArray, deleteArray);
}

/*In some function:*/
IntArray array;
int[] years = array.create(2);
years[0] = 2020;
years[1] = 2021;
array.trim(1);
unsigned int size = array.size; /*1 as 2020.*/
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