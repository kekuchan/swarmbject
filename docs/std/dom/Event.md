# "std::dom::Event" class:

Used to point to a DOM event. Multiple 
std::dom::Event objects can point to 
the same event.

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node input;
		std::html::InputElement::create(
			&document, &input);
		input.setOnKeyDown(onKeyDown);
		input.setOnCopy(onCopy);
		input.setOnPaste(onPaste);
		std::dom::Node node;
		std::html::Document::getBody(&document, &node);
		node.appendChild(&input);
	}
	
	static void onKeyDown(std::dom::Event* e,
		std::ApplicationInstance aexcl app){
	}
	
	static void onCopy(std::dom::Event* e,
		std::ApplicationInstance aexcl app){
	}
	
	static void onPaste(std::dom::Event* e,
		std::ApplicationInstance aexcl app){
	}
}
```

## "getCurrentTarget" member function:

Gets the current target of the event.

Parameters:
* A pointer to an std::dom::Node object, that 
this function sets to reference the target.

Returns: void.

```
/*In Main::onKeyDown.*/
std::dom::Node node;
e->getCurrentTarget(&node);
/*"node" now references the input element. */
```

## "getKeyCode" member function:

Gets the pressed key.

Returns: unsigned int.

```
/*In Main::onKeyDown.*/
unsigned int keyCode = e->getKeyCode();
```

## "getShiftKey" member function:

Checks if the shift key was 
pressed during the event.
	
Returns: true, if the shift key was 
pressed during the event, false otherwise.

```
/*In Main::onKeyDown.*/
bool shift = e->getShiftKey();
```

## "getTarget" member function:

Gets the target of the event.

Parameters:
* A pointer to an std::dom::Node object, that 
this function sets to reference the target.

Returns: void.

```
/*In Main::onKeyDown.*/
std::dom::Node node;
e->getTarget(&node);
/*"node" now references the input element. */
```

## "getTextClipboardData" member function:

Inserts the plain text data of the 
clipboard to an std::DString's end.

Parameters:
* A pointer an std::DString.

Returns: void.

```
/*In Main::onPaste.*/
std::DString string;
e->getTextClipboardData(&string);
```

## "preventDefault" member function:

Prevent the default action 
associated with the event.

Returns: void.

```
/*In Main::onPaste.*/
e->preventDefault();
/*The clipboard data is not inserted..*/
```

## "setTextClipboardData" member function:

Sets the plain text data of the 
clipboard to be a copy of a substring.

Parameters:
* The unsigned char array of the substring to copy.
* The starting index of the substring to copy 
in its array.
* The length of the substring to copy.

Returns: void.

```
/*In Main::onCopy.*/
e->setTextClipboardData("2021", 0, 4);
/*The clipboard now contains "2021".*/
```

## "stopPropagation" member function:

Stops the event from propagating further.

Returns: void.

```
/*In Main::onKeyDown.*/
e->stopPropagation();
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