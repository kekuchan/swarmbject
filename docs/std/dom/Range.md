# "std::dom::Range" class:

Used to point to a range of DOM nodes. 
Multiple std::dom::Range objects can 
point to the same range.

```
class Main {
	std::dom::Node text;
	
	void main(std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node* text = &app.main.text;
		std::dom::Text::create(
			&document, text, "2021", 0, 4);
		std::dom::Node input;
		std::html::InputElement::create(
			&document, &input);
		std::html::InputElement::setType(
			&input, std::html::InputTypes::button);
		std::html::InputElement::setValue(
			&input, "Click", 0, 5);
		input.setOnMouseDown(onMouseDown);
		std::dom::Node node;
		std::html::Document::getBody(&document, &node);
		node.appendChild(text);
		node.appendChild(&input);
	}
	
	static void onMouseDown(std::dom::Event* e,
		std::ApplicationInstance aexcl app){
		e->preventDefault();
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Selection selection;
		window.getSelection(&selection);
		std::dom::Range range;
		selection.getRangeAt(&range, 0);
	}
}
```

## "deleteContents" member function:

Deletes the range's content.

Returns: void.

```
/*In Main::onMouseDown.*/
range.deleteContents();
/*Selecting "2021", and clicking on 
	the button deletes it.*/
```

## "getCollapsed" member function:

Checks if the range's start and end 
is the same, as that indicates a 
position, instead of a whole range.

Returns: bool.

```
/*In Main::onMouseDown.*/
bool collapsed = range.getCollapsed();
/*Selecting "2021", and clicking on 
	the button returns false.*/
```

## "getEndContainer" member function:

Gets the range's ending container.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::onMouseDown.*/
std::dom::Node node;
range.getEndContainer(&node);
/*Selecting "2021", and clicking on the button 
	sets the node to point to the text node.*/
```

## "getEndOffset" member function:

Gets the range's ending offset in the 
ending container. For text nodes the 
offset is in UTF-8 unsigned chars.

Returns: unsigned int.

```
/*In Main::onMouseDown.*/
unsigned int offset = range.getEndOffset();
/*Selecting "2021", and clicking 
	on the button returns 4.*/
```

## "getStartContainer" member function:

Gets the range's starting container.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::onMouseDown.*/
std::dom::Node node;
range.getStartContainer(&node);
/*Selecting "2021", and clicking on the button 
	sets the node to point to the text node.*/
```

## "getStartOffset" member function:

Gets the range's starting offset in the 
starting container. For text nodes the 
offset is in UTF-8 unsigned chars.

Returns: unsigned int.

```
/*In Main::onMouseDown.*/
unsigned int offset = range.getStartOffset();
/*Selecting "2021", and clicking 
	on the button returns 0.*/
```

## "setEnd" member function:

Sets the range's ending container and 
offset. For text nodes the offset is 
in UTF-8 unsigned chars.

Parameters:
* The ending container as 
a pointer to an std::dom::Node.
* The ending offset.

Returns: void.

```
/*In Main::onMouseDown.*/
std::dom::Node* text = &app.main.text;
range.setStart(text, 0);
range.setEnd(text, 4);
/*Clicking on the button selects "2021".*/
```

## "setStart" member function:

Sets the range's starting container and 
offset. For text nodes the offset is 
in UTF-8 unsigned chars.

Parameters:
* The starting container as 
a pointer to an std::dom::Node.
* The starting offset.

Returns: void.

```
/*In Main::onMouseDown.*/
std::dom::Node* text = &app.main.text;
range.setStart(text, 0);
range.setEnd(text, 4);
/*Clicking on the button selects "2021".*/
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