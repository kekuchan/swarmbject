# "std::ds::Buffer" class:

Used to pack different types to an unsigned char 
array, where the total number of unsigned chars 
are known and not expected to be changing. 
Useful for example to handle binary file formats.

## "data" data member:

The contained data as an unsigned char array,
if direct manipulation is needed, instead of
the get and set functions.

```
std::ds::Buffer buffer;
buffer.setSize(1);
unsigned char[] data = buffer.data;
data[0] = 21;
```

## "size" data member:

As an unsigned int, the number of unsigned chars, 
that the buffer stores.

```
std::ds::Buffer buffer;
buffer.setSize(1);
unsigned int size = buffer.size; /*1*/
```

## "clear" member function:

Clears the buffer to its initial state. As 
it deletes the contained array, usage of 
the previous data member is not valid.

Returns: void.

```
std::ds::Buffer buffer;
buffer.setSize(1);
buffer.clear();
unsigned int size = buffer.size; /*0*/
```

## "getU8" member function:

Gets an unsigned char value from the buffer.

Parameters:
* The index of the value in the buffer.

Returns: unsigned char.

```
std::ds::Buffer buffer;
buffer.setSize(1);
buffer.setU8(0, 21);
unsigned char value = buffer.getU8(0); /*21*/
```

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
std::ds::Buffer buffer;
buffer.setSize(2);
buffer.setU8(0, 20);
buffer.setU8(1, 21);
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

```
std::ds::Buffer buffer;
buffer.setSize(2);
buffer.setU16BE(0, 2021);
unsigned short value = buffer.getU16BE(0); /*2021*/
```

## "getU16LE" member function:

Gets an unsigned short value from the buffer,
that was stored as a little endian (2 unsigned 
chars stored right to left).

Parameters:
* The index of the value in the buffer.

Returns: unsigned short.

```
std::ds::Buffer buffer;
buffer.setSize(2);
buffer.setU16LE(0, 2021);
unsigned short value = buffer.getU16LE(0); /*2021*/
```

## "getU32BE" member function:

Gets an unsigned int value from the buffer,
that was stored as a big endian (4 unsigned 
chars stored left to right).

Parameters:
* The index of the value in the buffer.

Returns: unsigned int.

```
std::ds::Buffer buffer;
buffer.setSize(4);
buffer.setU32BE(0, 20212021);
unsigned short value = buffer.getU32BE(0); /*20212021*/
```

## "getU32LE" member function:

Gets an unsigned int value from the buffer,
that was stored as a little endian (4 unsigned 
chars stored right to left).

Parameters:
* The index of the value in the buffer.

Returns: unsigned int.

```
std::ds::Buffer buffer;
buffer.setSize(4);
buffer.setU32LE(0, 20212021);
unsigned short value = buffer.getU32LE(0); /*20212021*/
```

## "move" member function:

Moves the data from another std::ds::Buffer.
The previous data is deleted.

Parameters:
* A pointer to the Buffer to move from.

Returns: void.

```
std::ds::Buffer first;
first.setSize(2);
first.setU16LE(0, 2020);
std::ds::Buffer second;
second.setSize(2);
second.setU16LE(0, 2021);
first.move(&second);
/*first=2021, second=*/
```

## "setSize" member function:

Changes the size of the buffer. As it creates a 
new array and copy all the elements, usage of 
the previous data member is not valid.

Parameters:
* The new size the buffer.

Returns: void.

```
std::ds::Buffer buffer;
buffer.setSize(1);
unsigned int size = buffer.size; /*1*/
buffer.setSize(2);
size = buffer.size; /*2*/
```

## "setU8" member function:

Sets an unsigned char value to the buffer.

Parameters:
* The index to set the value in the buffer.
* The unsigned char value to set.

Returns: void.

An example was already given at the 
"getU8" member function.

## "setU8s" member function:

Sets a sequence of unsigned char values
to the buffer.

Parameters:
* The starting index to set the values in the buffer.
* An array to copy the values from.
* The starting index in the array to copy the values from.
* The number of values to set.

Returns: void.

```
unsigned char[] values = new unsigned char[2];
values[0] = 20;
values[1] = 21;
std::ds::Buffer buffer;
buffer.setSize(2);
buffer.setU8s(0, values, 0, 2);
unsigned char value = buffer.getU8(0); /*20*/
value = buffer.getU8(1); /*21*/
```

## "setU16BE" member function:

Sets an unsigned short value to the buffer, as a 
big endian (2 unsigned chars stored left to right).

Parameters:
* The index to set the value in the buffer.
* The unsigned short value to set.

Returns: void.

An example was already given at the 
"getU16BE" member function.

## "setU16LE" member function:

Sets an unsigned short value to the buffer, 
as a little endian (2 unsigned chars stored 
right to left).

Parameters:
* The index to set the value in the buffer.
* The unsigned short value to set.

Returns: void.

An example was already given at the 
"getU16LE" member function.

## "setU32BE" member function:

Sets an unsigned int value to the buffer, as a
big endian (4 unsigned chars stored left to right).

Parameters:
* The index to set the value in the buffer.
* The unsigned int value to set.

Returns: void.

An example was already given at the 
"getU32BE" member function.

## "setU32LE" member function:

Sets an unsigned int value to the buffer, 
as a little endian (4 unsigned chars stored 
right to left).

Parameters:
* The index to set the value in the buffer.
* The unsigned int value to set.

Returns: void.

An example was already given at the 
"getU32LE" member function.

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