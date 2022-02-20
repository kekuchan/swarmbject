# "std::ds::DBuffer" class:

Used to pack different types to an unsigned char 
array, where the total number of unsigned chars 
are not yet known or expected to be changing, 
thus it is a dynamic buffer.

## "capacity" data member:

In order so that a new array doesn't have to be 
created each time when the number of unsigned chars 
changes, instead an array with a greater capacity 
might be created than what is currently needed,
thus a new array has to be created only when enough 
data is inserted so that a greater capacity is
needed. Stored as an unsigned int.

```
std::ds::DBuffer buffer;
unsigned int capacity = buffer.capacity; /*0*/
```
	
## "data" data member:

The contained data as an unsigned char array,
if direct manipulation is needed, instead of
the add and get functions.

```
std::ds::DBuffer buffer;
buffer.addU8(21);
unsigned char[] data = buffer.data;
unsigned char value = data[0]; /*21*/
```

## "size" data member:

As an unsigned int, the number of unsigned chars, 
that the buffer stores.

```
std::ds::DBuffer buffer;
buffer.addU8(21);
unsigned int size = buffer.size; /*1*/
```

## "addU8" member function:

Inserts an unsigned char value to the buffer's end.
This might require creating a new array and copy 
all the elements due to the capacity, making the 
usage of the previous data member not valid.

Parameters:
* The unsigned char value to insert.

Returns: void.
	
```
std::ds::DBuffer buffer;
buffer.addU8(21);
unsigned char value = buffer.getU8(0); /*21*/
```

## "addU8s" member function:

Inserts a sequence of unsigned char values 
to the buffer's end. This might require creating 
a new array and copy all the values due to the 
capacity, making the usage of the previous data 
member not valid.

Parameters:
* An array to copy the values from.
* The starting index in the array to copy the values from.
* The number of values to insert.

Returns: void.

```
unsigned char[] values = new unsigned char[2];
values[0] = 20;
values[1] = 21;
std::ds::DBuffer buffer;
buffer.addU8s(values, 0, 2);
unsigned char value = buffer.getU8(0); /*20*/
value = buffer.getU8(1); /*21*/
```

## "addU16BE" member function:

Inserts an unsigned short value to the buffer's 
end, as a big endian (2 unsigned chars stored 
left to right). This might require creating a 
new array and copy all the values due to the 
capacity, making the usage of the previous data 
member not valid.

Parameters:
* The unsigned short value to insert.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU16BE(2021);
unsigned short value = buffer.getU16BE(0); /*2021*/
```

## "addU16LE" member function:

Inserts an unsigned short value to the buffer's 
end, as a little endian (2 unsigned chars stored 
right to left). This might require creating a 
new array and copy all the values due to the 
capacity, making the usage of the previous data 
member not valid.

Parameters:
* The unsigned short value to insert.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU16LE(2021);
unsigned short value = buffer.getU16LE(0); /*2021*/
```

## "addU32BE" member function:

Inserts an unsigned int value to the buffer's 
end, as a big endian (4 unsigned chars stored 
left to right). This might require creating a 
new array and copy all the values due to the 
capacity, making the usage of the previous data 
member not valid.

Parameters:
* The unsigned int value to insert.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU32BE(20212021);
unsigned short value = buffer.getU32BE(0); /*20212021*/
```

## "addU32LE" member function:

Inserts an unsigned int value to the buffer's 
end, as a little endian (4 unsigned chars stored 
right to left). This might require creating a 
new array and copy all the values due to the 
capacity, making the usage of the previous data 
member not valid.

Parameters:
* The unsigned int value to insert.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU32LE(20212021);
unsigned short value = buffer.getU32LE(0); /*20212021*/
```

## "clear" member function:

Sets the buffer's size to 0.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU8(21);
buffer.clear();
unsigned int size = buffer.size; /*0*/
```

## "getU8" member function:

Gets an unsigned char value from the buffer.

Parameters:
* The index of the value in the buffer.

Returns: unsigned char.

An example was already given at the 
"addU8" member function.

## "getU8s" member function:

Gets a sequence of unsigned char values
from the buffer.

Parameters:
* The starting index of the values in the buffer.
* An array to copy the values to.
* The starting index in the array to copy the values to.
* The number of values to get.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU8(20);
buffer.addU8(21);
unsigned char[] values = new unsigned char[2];
buffer.getU8s(0, values, 0, 2);
unsigned char value = values[0]; /*20*/
value = values[1]; /*21*/
```

## "getU16BE" member function:

Gets an unsigned short value from the buffer,
that was stored as a big endian (2 unsigned 
chars stored left to right).

Parameters:
* The index of the value in the buffer.

Returns: unsigned short.

An example was already given at the 
"addU16BE" member function.

## "getU16LE" member function:

Gets an unsigned short value from the buffer,
that was stored as a little endian (2 unsigned 
chars stored right to left).

Parameters:
* The index of the value in the buffer.

Returns: unsigned short.

An example was already given at the 
"addU16LE" member function.

## "getU32BE" member function:

Gets an unsigned int value from the buffer,
that was stored as a big endian (4 unsigned 
chars stored left to right).

Parameters:
* The index of the value in the buffer.

Returns: unsigned int.

An example was already given at the 
"addU32BE" member function.

## "getU32LE" member function:

Gets an unsigned int value from the buffer,
that was stored as a little endian (4 unsigned 
chars stored right to left).

Parameters:
* The index of the value in the buffer.

Returns: unsigned int.

An example was already given at the 
"addU32LE" member function.

## "move" member function:

Moves the data from another std::ds::DBuffer.
The previous data is deleted.

Parameters:
* A pointer to the DBuffer to move from.

Returns: void.

```
std::ds::DBuffer first;
first.addU16LE(2020);
std::ds::DBuffer second;
second.addU16LE(2021);
first.move(&second);
/*first=2021, second=*/
```

## "reserve" member function:

Increases the capacity of the buffer. This 
requires creating a new array and copy all 
the values, making the usage of the previous 
data member not valid.

Parameters:
* The new capacity.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.reserve(2);
unsigned int capacity = buffer.capacity; /*2*/
unsigned int size = buffer.size; /*0*/
```

## "shrink" member function:

Decreases the capacity of the buffer. This 
requires creating a new array and copy 
the remaining values, making the usage 
of the previous data member not valid.

Parameters:
* The new capacity.

Returns: void.

```
std::ds::DBuffer buffer;
buffer.addU8(20);
buffer.addU8(21);
buffer.shrink(1);
unsigned int capacity = buffer.capacity; /*1*/
unsigned int size = buffer.size; /*1 as 20.*/
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