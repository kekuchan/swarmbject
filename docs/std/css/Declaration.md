# "std::css::Declaration" class:

Used to point to a CSS style declaration block.
Multiple std::css::Declaration objects can 
point to the same declaration block.

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
		std::css::Declaration style;
		std::html::Element::getStyle(&div, &style);
	}
}
```

## "isNull" member function:

Checks if the object points nowhere.
	
Returns: true, if the object points nowhere,
false otherwise.

```
/*In Main::main.*/
bool isNull = style.isNull();
/*false, as it points to the div's style.*/
```

## "setAlign" member function:

Sets the horizontal alignment.

Parameters:
* Either nullptr to unset, or a pointer 
to a std::css::Keyword object with an 
std::css::AlignTypes value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setAlign(keyword.set(
	std::css::AlignTypes::middle));
```

## "setBackgroundColor" member function:

Sets the background color.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::RGB object.

Returns: void.

```
/*In Main::main.*/
std::css::RGB rgb;
rgb.color.set(255, 255, 255);
style.setBackgroundColor(&rgb);
```

## "setBorderStyle" member function:

Sets the border style.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::BorderStyles value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setBorderStyle(keyword.set(
	std::css::BorderStyles::solid));
```

## "setBorderBottomStyle" member function:

Sets the border bottom style.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::BorderStyles value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setBorderBottomStyle(keyword.set(
	std::css::BorderStyles::solid));
```

## "setBorderLeftStyle" member function:

Sets the border left style.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::BorderStyles value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setBorderLeftStyle(keyword.set(
	std::css::BorderStyles::solid));
```

## "setBorderRightStyle" member function:

Sets the border right style.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::BorderStyles value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setBorderRightStyle(keyword.set(
	std::css::BorderStyles::solid));
```

## "setBorderTopStyle" member function:

Sets the border top style.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::BorderStyles value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setBorderTopStyle(keyword.set(
	std::css::BorderStyles::solid));
```

## "setBorderWidth" member function:

Sets the border width.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setBorderWidth(len.set(
	1, std::css::Units::px));
```

## "setBorderBottomWidth" member function:

Sets the border bottom width.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setBorderBottomWidth(len.set(
	1, std::css::Units::px));
```

## "setBorderLeftWidth" member function:

Sets the border left width.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setBorderLeftWidth(len.set(
	1, std::css::Units::px));
```

## "setBorderRightWidth" member function:

Sets the border right width.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setBorderRightWidth(len.set(
	1, std::css::Units::px));
```

## "setBorderTopWidth" member function:

Sets the border top width.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setBorderTopWidth(len.set(
	1, std::css::Units::px));
```

## "setDisplay" member function:

Sets the display type.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::DisplayTypes value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setDisplay(keyword.set(
	std::css::DisplayTypes::none));
```

## "setFontSize" member function:

Sets the font size.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setFontSize(len.set(
	21, std::css::Units::px));
```

## "setHeight" member function:

Sets the content's height, thus by default 
without the padding, border and margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setHeight(len.set(
	21, std::css::Units::px));
```

## "setLineHeight" member function:

Sets the line height.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setLineHeight(len.set(
	21, std::css::Units::px));
```

## "setMargin" member function:

Sets the margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::MarginTypes value, or a 
pointer to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setMargin(keyword.set(
	std::css::MarginTypes::auto));
```

## "setMarginBottom" member function:

Sets the bottom margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::MarginTypes value, or a 
pointer to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setMarginBottom(len.set(
	21, std::css::Units::px));
```

## "setMarginLeft" member function:

Sets the left margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::MarginTypes value, or a 
pointer to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setMarginLeft(len.set(
	21, std::css::Units::px));
```

## "setMarginRight" member function:

Sets the right margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::MarginTypes value, or a 
pointer to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setMarginRight(len.set(
	21, std::css::Units::px));
```

## "setMarginTop" member function:

Sets the top margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::MarginTypes value, or a 
pointer to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setMarginTop(len.set(
	21, std::css::Units::px));
```

## "setMinHeight" member function:

Sets the minimum height.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setMinHeight(len.set(
	21, std::css::Units::px));
```

## "setOverflow" member function:

Sets the overflow type.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::OverflowTypes value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setOverflow(keyword.set(
	std::css::OverflowTypes::auto));
```

## "setPadding" member function:

Sets the padding.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setPadding(len.set(
	21, std::css::Units::px));
```

## "setPaddingBottom" member function:

Sets the bottom padding.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setPaddingBottom(len.set(
	21, std::css::Units::px));
```

## "setPaddingLeft" member function:

Sets the left padding.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setPaddingLeft(len.set(
	21, std::css::Units::px));
```

## "setPaddingRight" member function:

Sets the right padding.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setPaddingRight(len.set(
	21, std::css::Units::px));
```

## "setPaddingTop" member function:

Sets the top padding.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setPaddingTop(len.set(
	21, std::css::Units::px));
```

## "setTabSize" member function:

Sets the tabulator size.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setTabSize(len.set(
	2, std::css::Units::integer));
```

## "setTextAlign" member function:

Sets the vertical alignment.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::TextAlignTypes value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setTextAlign(keyword.set(
	std::css::TextAlignTypes::center));
```

## "setWhiteSpace" member function:

Sets the white space type.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Keyword object with an 
std::css::TextAlignTypes value.

Returns: void.

```
/*In Main::main.*/
std::css::Keyword keyword;
style.setWhiteSpace(keyword.set(
	std::css::WhiteSpaceTypes::nowrap));
```

## "setWidth" member function:

Sets the content's width, thus by default 
without the padding, border and margin.

Parameters:
* Either nullptr to unset, or a pointer 
to an std::css::Short object.

Returns: void.

```
/*In Main::main.*/
std::css::Short len;
style.setWidth(len.set(
	21, std::css::Units::px));
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