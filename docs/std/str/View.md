# "std::str::View" class:

Used to create a const view of a substring, thus 
it only points to the substring, instead of making 
a copy of it.

## "data" data member:

The unsigned char array of the substring.

```
std::str::View string;
string.set("2021", 2, 2);
unsigned char const[] data = string.data;
/*The view is only '2','1', but the data is "2021".*/
```
	
## "length" data member:

The number of unsigned chars of the substring.
This is not nessesary the same as the number 
of characters in the string, as with UTF-8, 
a character can use 1-4 unsigned chars.

```
std::str::View string;
string.set("2021", 2, 2);
unsigned int length = string.length; /*2*/
```

## "start" data member:

The starting index of the substring 
in its array.

```
std::str::View string;
string.set("2021", 2, 2);
unsigned int start = string.start; /*2*/
```

## "clear" member function:

Clears the view to its initial state.

Returns: void.

```
std::str::View string;
string.set("2021", 2, 2);
string.clear();
unsigned int length = string.length; /*0*/
```

## "compare" member function:

Compares the substring to another substring.

Parameters:
* The unsigned char array of the 
substring to compare with.
* The starting index of the substring 
to compare with in its array.
* The length of the substring to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::View first;
first.setCString("YEAR");
unsigned char const[] second = "year";

unsigned char compare = first.compare(
	second, 0, 4, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compare(
	second, 0, 4, &cmp);
/*std::Compare::equal.*/
```

## "compareCString" member function:

Compares the substring to a 0 ended 
unsigned char array string.

Parameters:
* The 0 ended unsigned char array string 
to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::View first;
first.setCString("YEAR");
unsigned char const[] second = "year";

unsigned char compare = 
	first.compareCString(second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareCString(second, &cmp);
/*std::Compare::equal.*/
```

## "compareDString" member function:

Compares the substring to an std::str::DString.

Parameters:
* A pointer to the DString to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::View first;
first.setCString("YEAR");
std::str::DString second;
second.addCString("year");

unsigned char compare = 
	first.compareDString(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareDString(&second, &cmp);
/*std::Compare::equal.*/
```

## "compareString" member function:

Compares the substring to an std::str::String.

Parameters:
* A pointer to the String to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::View first;
first.setCString("YEAR");
std::str::String second;
second.setCString("year");

unsigned char compare = 
	first.compareString(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareString(&second, &cmp);
/*std::Compare::equal.*/
```

## "compareView" member function:

Compares the substring to an std::str::View.

Parameters:
* A pointer to the std::str::View to compare with.
* Either nullptr, or a pointer to an 
std::str::Compare object, with its compare member 
pointing to a function that compares a character 
or more of its src and dst members, from their 
starting index, returning an std::Compare value, 
and setting their starting and ending + 1 indices.

Returns: an std::Compare value.

```
std::str::View first;
first.setCString("YEAR");
std::str::View second;
second.setCString("year");

unsigned char compare = 
	first.compareView(&second, nullptr);
/*std::Compare::less, as 'Y' < 'y'.*/

std::str::Compare cmp;
cmp.compare = std::str::Compare::rangeCI;
compare = first.compareView(&second, &cmp);
/*std::Compare::equal.*/
```

## "set" member function:

Sets the view to point to a substring.

Parameters:
* The unsigned char array of the substring 
to point to.
* The starting index of the substring 
to point to in its array.
* The length of the substring to copy to point to.

Returns: void.

```
std::str::View string;
string.set("2021", 2, 2);
/*'2','1'*/
```
		
## "setCString" member function:

Sets the view to point to a 0 ended 
unsigned char array string.

Parameters:
* The 0 ended unsigned char array string.

Returns: void.

```
std::str::View string;
string.setCString("2021");
/*'2','0','2','1'*/
```

## "setDString" member function:

Sets the view to point to 
an std::str::DString data.

Parameters:
* A pointer to the std::str::DString.

Returns: void.

```
std::str::DString year;
year.setCString("2021");
std::str::View string;
string.setDString(&year);
/*'2','0','2','1'*/
```

## "setString" member function:

Sets the view to point to 
an std::str::String data.

Parameters:
* A pointer to the std::str::String.

```
std::str::String year;
year.setCString("2021");
std::str::View string;
string.setString(&year);
/*'2','0','2','1'*/
```

Returns: void.

## "setView" member function:

Sets the view to point to the same 
substring as another std::str::View.

Parameters:
* A pointer to the std::str::View.
	
Returns: void.

```
std::str::View year;
year.setCString("2021");
std::str::View string;
string.setView(&year);
/*'2','0','2','1'*/
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