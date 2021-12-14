# "std::dom::Node" class:

Used to point to a DOM nodes. Multiple 
std::dom::Node objects can point to 
the same node.

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
		std::dom::Node div;
		std::html::DivElement::create(
			&document, &div);
		std::dom::Node node;
		std::html::Document::getBody(&document, &node);
		node.appendChild(&input);
		node.appendChild(&div);
	}
}
```

## "appendChild" member function:

Inserts a node to the node's end.

Parameters:
* A pointer to the node, as an std::dom::Node.

Returns: void.

```
/*In Main::main.*/
div.appendChild(&input);
/*Now the div contains the input, 
	instead of the document body.*/
```
	
## "getChildNode" member function:

Gets a contained node from the node.

Parameters:
* A pointer to an std::dom::Node to set.
* The index of the node to get.

Returns: void.

```
/*In Main::main.*/
node.getChildNode(&node, 1);
/*The node now points to the div.*/
```

## "getChildNodesLength" member function:

Gets the number of nodes in the node.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int length = 
	node.getChildNodesLength(); /*2*/
```
	
## "getFirstChild" member function:

Gets the first contained node from the node.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::main.*/
node.getFirstChild(&node);
/*The node now points to the input.*/
```
	
## "getLastChild" member function:

Gets the last contained node from the node.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::main.*/
node.getLastChild(&node);
/*The node now points to the div.*/
```
	
## "getNextSibling" member function:

Gets the node after the node.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::main.*/
input.getNextSibling(&node);
/*The node now points to the div.*/
```
	
## "getNodeType" member function:

Gets the node's type, as an 
std::dom::NodeTypes value.

Returns: unsigned int.

```
/*In Main::main.*/
unsigned int type = div.getNodeType();
/*std::dom::NodeTypes::element*/
```
	
## "getParentNode" member function:

Gets the container node.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::main.*/
div.getParentNode(&node);
/*The node points to the document body.*/
```
	
## "getPreviousSibling" member function:

Gets the node before the node.

Parameters:
* A pointer to an std::dom::Node to set.

Returns: void.

```
/*In Main::main.*/
div.getPreviousSibling(&node);
/*The node now points to the input.*/
```
	
## "insertBefore" member function:

Inserts a node before another node.

Parameters:
* A pointer to an std::dom::Node to insert.
* A pointer to an std::dom::Node to insert before.

Returns: void.

```
/*In Main::main.*/
node.insertBefore(&div, &input);
/*The div is now before the input instead of after.*/
```
	
## "isNull" member function:

Checks if the object points nowhere.
	
Returns: true, if the object points nowhere,
false otherwise.

```
/*In Main::main.*/
bool isNull = div.isNull();
/*false, as it points to the div element.*/
```
	
## "isNullStatic" static function:

Checks if an std::dom::Node 
object points nowhere.

Parameters:
* A pointer to an std::dom::Node object.

Returns: true, if the object points nowhere,
false otherwise.

```
/*In Main::main.*/
bool isNull = 
	std::dom::Node::isNullStatic(&div);
/*false, as it points to the div element.*/
```

## "isSameNode" member function:

Checks if another objects points to the same node.

Parameters:
* A pointer to an std::dom::Node object to check.

Returns: true, if the object points 
to the same node, false otherwise.

```
/*In Main::main.*/
bool same = div.isSameNode(&input); /*false*/
```

## "removeChild" member function:

Removes a contained node from the node.

Parameters:
* A pointer to an std::dom::Node object to remove.

Returns: void.

```
/*In Main::main.*/
node.removeChild(&div);
```
	
## "replaceChild" member function:

Replaces a contained node with another.

Parameters:
* A pointer to an std::dom::Node object to replace with.
* A pointer to an std::dom::Node object to replace.

Returns: void.

```
/*In Main::main.*/
node.removeChild(&div);
node.replaceChild(&div, &input);
/*The node now contains only the div.*/
```

## "scrollIntoView" member function:

Scrolls the element into view.

Returns: void.

```
/*In Main::main.*/
div.scrollIntoView();
```

## "set" member function:

Sets the object to point to the given node.

Parameters:
* A pointer to an std::dom::Node object to copy.

Returns: void.

```
/*In Main::main.*/
node.set(&div);
/*The node now points to the div.*/
```

## "setContentEditable" member function:

Sets element's content to be editable or not.

Parameters:
* A bool value to set the content editable or not.

Returns: void.

```
/*In Main::main.*/
div.setContentEditable(true);
```

## "setOnChange" member function:

Sets a function to be called each 
time the content is changed.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onChange(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnChange(onChange);
```

## "setOnClick" member function:

Sets a function to be called after 
each mouse click or tap.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onClick(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnClick(onClick);
```

## "setOnCopy" member function:

Sets a function to be called each 
time when content is copied.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onCopy(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnCopy(onCopy);
```

## "setOnCut" member function:

Sets a function to be called each 
time when content is cut.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onCut(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnCut(onCut);
```

## "setOnKeyDown" member function:

Sets a function to be called each 
time a key is pressed.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onKeyDown(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnKeyDown(onKeyDown);
```

## "setOnMouseDown" member function:

Sets a function to be called each 
time a mouse button is pressed or on a tap.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onMouseDown(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnMouseDown(onMouseDown);
```

## "setOnPaste" member function:

Sets a function to be called each 
time when content is pasted.

Parameters:
* Either nullptr to unset, or a 
pointer to a "void(std::dom::Event*, 
std::ApplicationInstance)" function to call.

Returns: void.

```
/*In Main.*/
static void onPaste(std::dom::Event* e,
	std::ApplicationInstance aexcl app){
}
/*In Main::main.*/
div.setOnPaste(onPaste);
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