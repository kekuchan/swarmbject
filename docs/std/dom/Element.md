# "std::dom::Element" class:

Static functions to work with DOM elements.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node div;
		std::html::DivElement::create(
			&document, &div);
		std::dom::Node node;
		std::html::Document::getBody(&document, &node);
		node.appendChild(&div);
	}
}
```

## "getClientHeight" static function:

Gets the element's height with the 
padding, but without the border, margin 
and the overflowed content.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int height = 
	std::dom::Element::getClientHeight(&div);
```

## "getClientLeft" static function:

Gets the element's left border's width.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int left = 
	std::dom::Element::getClientLeft(&div);
```

## "getClientTop" static function:

Gets the element's top border's height.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int top = 
	std::dom::Element::getClientTop(&div);
```

## "getClientWidth" static function:

Gets the element's width with the 
padding, but without the border, margin 
and the overflowed content.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int width = 
	std::dom::Element::getClientWidth(&div);
```

## "getScrollHeight" static function:

Gets the element's height with the 
padding and the overflowed content, 
but without the border and margin.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int height = 
	std::dom::Element::getScrollHeight(&div);
```

## "getScrollLeft" static function:

Gets the element's vertical scrolling position.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int left = 
	std::dom::Element::getScrollLeft(&div);
```

## "getScrollTop" static function:

Gets the element's horizontal scrolling position.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int top = 
	std::dom::Element::getScrollTop(&div);
```

## "getScrollWidth" static function:

Gets the element's width with the 
padding and the overflowed content, 
but without the border and margin.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int width = 
	std::dom::Element::getScrollWidth(&div);
```

## "getTagName" static function:

Copy the element's tag name to an array.
		
Parameters:
* A pointer to the element, as an std::dom::Node.
* The unsigned char array to copy to.
* The starting index of the array to copy to.

Returns: the length of the tag name.

```
/*In Main::main.*/
unsigned int length = 
	std::dom::Element::getTagName(
		&div, nullptr, 0));
std::str::DString string;
std::dom::Element::getTagName(
	&div, string.create(length), 0);
/*"DIV"*/
```

## "getTagNameDString" static function:

Inserts the element's tag name to an 
std::str::DString's end.

Parameters:
* A pointer to the element, as an std::dom::Node.
* A pointer an std::str::DString.

Returns: void.

```
/*In Main::main.*/
std::str::DString string;
std::dom::Element::getTagNameDString(
	&div, &string);
/*"DIV"*/
```

## "scrollIntoView" static function:

Scrolls the element into view.

Parameters:
* A pointer to the element, as an std::dom::Node.

Returns: void.

```
/*In Main::main.*/
std::dom::Element::scrollIntoView(&div);
```

## "setScrollLeft" static function:

Sets the element's vertical scrolling position.

Parameters:
* A pointer to the element, as an std::dom::Node.
* The position to set as an unsigned int.

Returns: void.

```
/*In Main::main.*/
std::dom::Element::setScrollLeft(
	&div, 21);
```

## "setScrollTop" static function:

Sets the element's horizontal scrolling position.

Parameters:
* A pointer to the element, as an std::dom::Node.
* The position to set as an unsigned int.

Returns: void.

```
/*In Main::main.*/
std::dom::Element::setScrollTop(
	&div, 21);
```

# Software license

Copyright (c) 2021, 2024 SWARMBJECT contributors

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

Copyright (c) 2021, 2024 SWARMBJECT contributors

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