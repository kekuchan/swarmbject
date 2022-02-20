# "std::str::Compare" class:

Used to compare strings. 

## "src" data member:

The unsigned char array of the first string.

## "srcMin" data member:

The lowest index of the first string that can 
be used when more that one unsigned char of 
the first string is compared.

## "srcStart" data member:

An index of a character 
of the first string to compare.

## "srcEnd" data member:

The starting index of the next character 
of the first string after the comparison.

## "srcMax" data member:

The highest index + 1 of the first string that 
can be used when more that one unsigned char 
of the first string is compared.

## "dst" data member:

The unsigned char array of the second string.

## "dstMin" data member:

The lowest index of the second string that can 
be used when more that one unsigned char of 
the second string is compared.

## "dstStart" data member:

An index of a character of the second 
string to compare, or if there is no second 
string, then the character to compare.

## "dstEnd" data member:

The starting index of the next character 
of the second string after the comparison.

## "dstMax" data member:

The highest index + 1 of the second string that 
can be used when more that one unsigned char 
of the second string is compared.

## "right" data member:

True if the strings are compared from left 
to right, false if compared from right to left.

## "compare" data member:

A pointer to a function that can be called with an 
std::str::Compare object, to compare a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

## "equalsCharCI" static function:

Compares in a case insensitive way the character 
stored in dstStart with a character or more of 
its src member, from its starting index, 
setting its starting and ending + 1 indices.

Parameters:
* A pointer to an std::str::Compare object.

Returns: std::Compare::equal if equal, 
or something else otherwise.

```
unsigned char const[] first = "YEAR";
unsigned char second = 'y';

std::str::Compare cmp;
cmp.setChar(first, 0, 4, second);
cmp.srcStart = 0;
unsigned char compare = 
	std::str::Compare::equalsCharCI(&cmp);
/*compare=std::Compare::equal,
srcStart=0, srcEnd=1*/
```

## "equalsCI" static function:

Compares in a case insensitive way a 
character or more of its src and dst members, 
from their starting index, setting their 
starting and ending + 1 indices.

Parameters:
* A pointer to an std::str::Compare object.

Returns: std::Compare::equal if equal, 
or something else otherwise.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

std::str::Compare cmp;
cmp.set(first, 0, 4, second, 0, 4);
cmp.srcStart = 0;
cmp.dstStart = 0;
unsigned char compare = 
	std::str::Compare::equalsCI(&cmp);
/*compare=std::Compare::equal,
srcStart=0, srcEnd=1, dstStart=0, dstEnd=1*/
```

## "rangeCI" static function:

Compares in a case insensitive way a 
character or more of its src and dst members, 
from their starting index, setting their 
starting and ending + 1 indices.

Parameters:
* A pointer to an std::str::Compare object.

Returns: an std::Compare value.

```
unsigned char const[] first = "dst";
unsigned char const[] second = "SRC";
unsigned char const[] third = "src";

std::str::Compare cmp;
cmp.set(first, 0, 3, second, 0, 3);
cmp.srcStart = 0;
cmp.dstStart = 0;
unsigned char compare = 
	std::str::Compare::rangeCI(&cmp);
/*compare=std::Compare::less,
srcStart=0, srcEnd=1, dstStart=0, dstEnd=1*/

cmp.set(second, 0, 3, third, 0, 3);
cmp.srcStart = 0;
cmp.dstStart = 0;
compare = std::str::Compare::rangeCI(&cmp);
/*compare=std::Compare::equal,
srcStart=0, srcEnd=1, dstStart=0, dstEnd=1*/
```

## "set" member function:

Sets the Compare object for 
string to string comparison.

Parameters:
* The "src" data member to set.
* The "srcMin" data member to set.
* The "srcMax" data member to set.
* The "dst" data member to set.
* The "dstMin" data member to set.
* The "dstMax" data member to set.
* The "right" data member to set.

Returns: void.

```
unsigned char const[] first = "YEAR";
unsigned char const[] second = "year";

std::str::Compare cmp;
cmp.set(first, 0, 4, second, 0, 4, true);
```

## "setChar" member function:

Sets the Compare object for 
string to character comparison.

Parameters:
* The "src" data member to set.
* The "srcMin" data member to set.
* The "srcMax" data member to set.
* The "dstStart" data member to set.
* The "right" data member to set.

Returns: void.

```
unsigned char const[] first = "YEAR";
unsigned char second = 'y';

std::str::Compare cmp;
cmp.setChar(first, 0, 4, second, true);
```

## "sortCI" static function:

Compares in a case insensitive way, 
but still sorting if equal, a character 
or more of its src and dst members, 
from their starting index, setting their 
starting and ending + 1 indices, 

Parameters:
* A pointer to an std::str::Compare object.

Returns: an std::Compare value.

```
unsigned char const[] first = "dst";
unsigned char const[] second = "SRC";
unsigned char const[] third = "src";

std::str::Compare cmp;
cmp.set(first, 0, 3, second, 0, 3);
cmp.srcStart = 0;
cmp.dstStart = 0;
unsigned char compare = 
	std::str::Compare::sortCI(&cmp);
/*compare=std::Compare::less,
srcStart=0, srcEnd=1, dstStart=0, dstEnd=1*/

cmp.set(second, 0, 3, third, 0, 3);
cmp.srcStart = 0;
cmp.dstStart = 0;
compare = std::str::Compare::sortCI(&cmp);
/*compare=std::Compare::less,
srcStart=0, srcEnd=1, dstStart=0, dstEnd=1*/
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