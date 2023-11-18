# Architecture

A SWARMBJECT application consists of a hierarchy of instances,
that can be distributed through multiple computers.
Note: This is a future goal, as currently 
only one instance is supported.
Each instance can contain multiple threads of execution.
During its run, the application can create asynchronous 
(independent) objects, each assigned to a thread.
An async object can contain data, that other async objects
can not access, and it can communicate with other
async objects by calling their named async functionalities.
Note: The way that async objects can only 
access their own data, but not others, was a
design choice, since these objects might not be
in the same computer, making such access inefficient,
furthermore due to asynchronity, multiple async 
objects could try to access the same data at the
same time, called a data race, that can result in 
unexpected behaviour. Instead by calling async 
functions, the callee does not have to wait for the call
to run, as that will be executed independently,
and each thread can execute only one async function
at the same time, while any others in the same thread
has to wait, making data races not possible.

# Tutorial

Note: This tutorial presents a short, but still a
more complex example, to show a rough overview of a
SWARMBJECT application. It is okay, if you don't fully 
grasp all the details, as the language and the API
references after it will explain the building blocks.

Lets create an application that models a situation, where
a manager gives a calculating task to a scientist, and
expects the result back when it is done, and instructs
a marketeer to display it to us, the Boss.

Download SWARMBJECT.html, SWARMBJECT.js and std.saf from the
releases to a folder on your device, and open the html.
To access the menu, tap or click the top colored header bar.
Create a folder for the tutorial with "Browse", "/",
"New folder", name it "tut", and choose "Create".
In the same way create a folder named "src" ("/tut/",
"New folder", Name: "src", "Create"). Upload the 
downloaded "std.saf" file to it ("/tut/src/",
"Upload"). ".saf" is a SWARMBJECT archive file,
a custom, but very simple format to pack multiple
files and folders into a single file.
Now create a file named "Main.scf"
("/tut/src/", "New file", Name: "Main.scf",
"Create"). Tap or click on "Main.scf",
and choose "Select", to open the file for editing.
Tap or click in the empty bordered area below
the top bar and type in the code:

```
class Main {
	void main(std::ApplicationInstance aexcl app){
		Manager aptr manager = new(app, 0) Manager;
		manager.start(app);
	}
}
```

The code of a SWARMBJECT application has a well defined
structure. It has to be in SWARMBJECT class files (".scf"),
in a folder named "src". Each file defines a class,
that objects can be created from. When the application
starts, it automatically creates an
"std::ApplicationInstance" async object. When a class 
file is not directly in the src folder, but in a
sub folder, then the "::" token is used. Thus the
"ApplicationInstance.scf" file is in the "std" folder,
but the programming term for it is that the
"ApplicationInstance" class is in the "std" namespace.
The "std" namespace contains the standard pre-programmed 
functionalities of the language, thus it is the API.
Async objects can contain non-async objects as their
data, so other async objects can not access these.
The "std::ApplicationInstance" async object 
contains a non-async "Main" object. This was a
design choice to be able to extend the
"std::ApplicationInstance" class with custom
data through the "Main" class, since many
functionalities are only available through the
"std::ApplicationInstance" class. The "Main" object
has to have a "main" function, that is called by the
"std::ApplicationInstance" object at the application
start, with also passing a reference to itself named as
the "app" parameter. The "aexcl" specifier indicates
that it is possible to access its members (data and
functions), since "main" is a function of the
"Main" object, that is part of the
"std::ApplicationInstance" object. The "main"
function creates a new "Manager" async object, and
a reference to it is stored in the "manager" variable.
The "aptr" specifier indicates, that it is not
possible to access its data from the "main" function,
as it is another async object, thus not part of the
"std::ApplicationInstance" async object, since
while async objects can contain non-async objects,
but can not contain other async objects, only
references to them. Thus async objects are always
independent. The parameters of the "new" operator
specified that the new "Manager" async object
is assigned to thread 0 (this is the first thread,
as indexing starts with 0) of the same instance as the
"app" object. In order for the "Manager" async 
object to start doing its job, its "start" async 
function is called, with the reference to the
"app" object, as the manager will need it later,
to display the result.

Tap or click the top header bar ("/tut/src/Main.scf") 
to open the menu again, and choose "Save opened file".
Now create "Manager.scf" in "src", the same 
way as "Main.scf", with the code:

```
async class Manager {

	std::ApplicationInstance aptr instance;
	
	async void start(
		std::ApplicationInstance aptr app){
		instance = app;
		Scientist aptr scientist = new(app, 1) Scientist;
		scientist.calculate(this);
	}
	
	async void calculated(
		unsigned int result){
		Marketeer aptr marketeer =
			new(instance, 1) Marketeer;
		marketeer.display(result, instance);
	}
}
```

The "start" function is async, as async objects 
can only communicate with async functions, while 
non-async functions, like the "main" function 
can only be used in the same async object. The 
"start" async function stores the "app" reference
in the "instance" data member of the "Manager" async 
object. A new "Scientist" async object is created 
in thread 1, and stored in the "scientist" variable.
The "app" parameter, the "instance" data member
and the "scientist" variable is "aptr", since 
the "Manager" object can only reference, but
not access their data. The scientist is instructed 
to calculate, by calling its async function with
a reference to the manager, as the "this" keyword 
always points to the associated object of the 
current function. The "calculated" async 
function will be called by the scientist with the
result, that is a positive (unsigned) integer, to be
sent to a marketeer in thread 1, in order to display 
it in the instance.

Create "Scientist.scf" in "src", with the code:

```
async class Scientist {

	async void calculate(
		Manager aptr manager){
		unsigned int result;
		/*After a long and complicated calculation.*/
		result = 2021;
		manager.calculated(result);
	}

}
```

The scientist calculates the result, and calls the 
"calculated" async function of the manager.

Save the file, and create "Marketeer.scf"
in "src", with the code:

```
async class Marketeer {

	async void display(
		unsigned int result,
		std::ApplicationInstance aptr app){
		onScreen(result, app);
	}

	static async void onScreen(
		unsigned int result,
		std::ApplicationInstance aexcl app){
		std::bom::Window window;
		app.getWindow(&window);
		std::dom::Node document;
		window.getDocumentNode(&document);
		std::dom::Node body;
		std::html::Document::getBody(&document, &body);
		std::str::DString string;
		string.addUint(result,
			std::NumberBases::decimal);
		std::dom::Node text;
		std::dom::Text::create(&document, &text,
			string.data, 0, string.length);
		body.appendChild(&text);
	}

}
```

The marketeer decided that the result is most impactful,
if it is displayed on the screen. However to do that, 
accessing "std::ApplicationInstance" data that 
"Marketeer" can't is needed. Adding an async function 
to "std::ApplicationInstance" would be needed, 
however that file should not be edited, since it is
part of the API. To solve this, a static async function 
can be used. Functions declared as static don't have
an associated object, thus they can access only the 
function parameters, while non-static functions can also 
access the associated object's data. This is how
the "calculated" function can access the "instance" 
data member of the manager, since it is a non-static 
function having the manager object associated with it.
A static async function by not having an associated 
object, can have an "aexcl" parameter instead, making
the function to run on that parameter's thread, 
and accessing its data. Thus the "onScreen" function 
can access the "app" data. This function uses the
BOM, DOM and HTML web standard, describing the structure 
of documents as a hierarchy of nodes, that a web 
browser displays. The objects and functions used in 
"onScreen" are non-async, for performance reasons.
The "getWindow" function sets the referenced 
"window" object, to point to the graphical window 
of the instance. The "&" addressof operator is used
to give the function a reference to the non-async 
"window" object. The "document" object is set to 
point to document that the window displays. The
content of the document is in its body node,
and the "body" object is set to point to it. 
The "result" is a number, that has to be converted 
to a string (textual data). A text node is created
from the string, containing the full length of its 
data, and it is appended to the body of the document,
for the browser to display it.

Save the file, and create "Compile.scf"
in "src", with the code:

```
class Compile : std::cmpl::Default {

	unsigned char constexpr threads = 2;

}
```

This sets the number of additional threads 
to use (besides the first thread) to 2, while 
leaving the other compiler settings as default.

Save the file, and in the menu, choose "Compile",
"/", "..", "/tut/", "Select". Use "Compile" under
the selected path, and wait until it finishes. 
Then choose "Run" at the bottom. This requires 
a popup, and the browser might ask you to allow it.

# Backups

Creating a backup as a safety measure is done with
"Browse" in the menu, navigate to a folder, choose
its path, and "Download". Now if the folder is
deleted, like by choosing its path, and "Delete",
it can be uploaded back by choosing a folder path
and "Upload" the backup file.

# Language reference:

## Comments:

Comments are notes written in the code, that will
be ignored by the compiler. Useful to provide
additional information about the code, to those
reading it.

### Single line comments:

When the // characters are used, everything
after it, until the end of the line 
constitutes as the comment.

```
//This is a single line comment.
```

### Multi line comments: When the /* characters are
used, everything after it, until the */ characters 
constitutes as the comment.

```
/*This is a
  multi line comment.*/
```

## Literals:

Literals are concrete values written in the code.

### Boolean literal:

Either *true* or *false*.

### Character literal:

Indicates a single character. The syntax 
(the way it has to be used) is: 'character'.

```
'c', 'h', 'a', 'r' /*character literals*/
```

There are a few special characters:

```
'\n' /*new line character*/
'\r' /*carriage return character*/
'\t' /*tabulator character*/
```

Due to its usage, the \ character is called
as the escaping character. Any other character
after it constitutes as just that character,
allowing to use the ' and the \ characters, 
or */ in a comment, without it closing the
comment.

```
'\'' /*' character*/
'\\' /*\ character*/
/*Even after \*/, the comment continues.*/
```

### String literal:

A string is a sequence of characters. 
The syntax is: "characters".

```
"This is a string."
```

A long string can be split, to improve
its readability in the code.

```
"A very long string."

/*is the same as:*/

"A "
"very "
"long "
"string."
```

To use the " character inside the string, it
has to be escaped.

```
"A \" character."
```

The characters of the string are encoded based
on the UTF-8 standard.

Note for beginners: To represent data, we can
start from a very simple element, the bit, that
can be either 0 or 1. With 2 bits the numbers
0-3 can be represented (0 as 00, 1 as 01,
2 as 10, 3 as 11). Continuing this way until
8 bits, known as a byte, the numbers 0-255
can be represented (0 as 00000000, ...,
255 as 11111111). So far the sequence of bits, 
were used to represent decimal numbers, however
they could also be used to represent characters
instead. How a character is corresponded to a
sequence of bits is called a character encoding. 
One of the most known is the ASCII standard,
that uses 7 bits to represent the most used 
characters in english texts. As international texts 
use many other characters, UTF-8 uses 1-4
bytes for a character, while staying compatible
with the ASCII standard.

The encoding of the string ends with a 0 byte.
The reason for this is that this way algorithms 
can iterate through the characters of the string,
and know that the string's end was reached 
when reading a 0 byte.

### Integer literal:

Indicates an integer number.

When starting with a non-zero, it is read as
a decimal integer.

```
2021 /*decimal integer*/
```

When starting with a 0x, it is read as
a hexadecimal integer.

```
0x7E5 /*2021 as a hexadecimal integer*/
```

When starting with a 0b, it is read as
a binary integer.

```
0b11111100101 /*2021 as a binary integer*/
```

Otherwise when starting with a 0, it is read as
an octal integer.

```
03745 /*2021 as an octal integer*/
```

### Floating literal:

Indicates a floating point number.

```
20.21 /*floating literal*/
```

### nullptr literal:

The SWARMBJECT language has constructs that point
to other constructs. *nullptr* indicates that such
a pointer points to nowhere. Pointers will be
explained more later in the manual.

### this literal:

The *this* literal points to the current object.
This will be explained more later in the manual.

# Data types:

Data can be stored in named constructs, having some 
associated type, that specifies what they can store.
The names of constructs, are of english letters (A-Z, 
a-z) and digits (0-9), but can not start with a digit.

## void:

Indicates an unspecified type, usable with pointers 
and functions, as explained later in the manual.

## bool:

Either *true* or *false*.

```
bool check = true;
/* The construct is named check, having a 
boolean type, and storing the value "true". */
```

Note: While only 1 bit is enough to store a boolean 
value, however it might use more, or even less 
(like due to some compression), as what is optimal 
depends on the platform, and that is also true for 
the other types. Thus the SWARMBJECT language does 
not define precise sizes, but only a range of values. 
Storing a value outside of the specified range might 
be possible, but unsafe, thus has to be avoided. As
a future goal, there might be some compiler settings 
to tell what it should optimize for.

## unsigned char:

An integer between 0 and 255. The name "char"
indicates, that it can store an ASCII character.

```
unsigned char newline = '\n';
unsigned char year = 21;
```

## char:

An integer between -128 and 127.

```
char year = -21;
```

## unsigned short:

An integer between 0 and 65535.

```
unsigned short year = 2021;
```

## short:

An integer between -32768 and 32767.

```
short year = -2021;
```

## unsigned int:

An integer between 0 and 4294967295.

```
unsigned int year = 20212021;
```

## int:

An integer between -2147483648 and 2147483647.

```
int year = -20212021;
```

## float:

A single precision floating point number.

```
float number = 20.21;
```

## double:

A double precision floating point number.

```
double number = 20.21/*and a lot more digits*/;
```

## Pointer:

A pointer is a construct, that points to some 
other construct, or even to itself. Its syntax is
that there is a * character after the type it 
can point to. A pointer that does not point 
anywhere has a nullptr value.

```
unsigned short* ptr = nullptr;
/*ptr can point to unsigned short types,
but does not point anywhere so far.*/
unsigned short year = 21;
ptr = &year;
/*ptr is set to point to the year. Simply using
year would mean to use just its value, while 
the & operator creates a pointer to the year 
construct itself. Thus the & is needed as 
"ptr = year;" is the same as "ptr = 21;", and 
in SWARMBJECT only pointers can be assigned to 
pointers, and 21 is an integer not a pointer.*/
*ptr = 2021;
/*Using *ptr refers to what ptr is pointing to,
instead of the ptr itself. As ptr points to the
year construct, its value is changed, thus year 
now contains 2021, instead of 21. */
```

Note: Pointers are useful, since code works with 
only the named constructs used in it, however 
with pointers it can work with anything that the
pointer can point to. Like in the example, simply 
"year = 2021;" could be used, but "*ptr = 2021;" 
also works when ptr points to some unsigned short 
other than the the year. Though if that is not 
needed, then not using the pointer is more efficient.

Note: It is the programmers duty to make sure that 
the pointers point to something valid, when used.

## array pointer:

An array is a construct that contains a sequence 
of same typed elements. An array pointer points
to such an array. Its syntax is that there is a [] 
after the type of the array's elements.

```
unsigned char const[] string =
	"This is a string.";
/*A string contains sequence of chars, thus it
is an array. As it is a literal, its elements 
can not be changed indicated by the const specifier.*/
unsigned char letter = string[0];
/*string[0] is used to access the element of the 
array at index 0, and since array indexing starts 
with 0, letter now contains the value 'T'.*/
letter = string[1];
/*letter now contains the value 'h'.*/
```

## class:

A class is a construct, that objects can be 
created from. Classes and objects are explained 
later in the manual.

## function pointer:

Classes can have named functionalities, that 
can be either called directly with that name,
or indirectly by a function pointer, that
points to it. Useful for the same reason as 
a pointer is. Function pointers are detailed
later in the manual.

# Classes and objects:

A class is an abstract construct from which many 
concrete constructs (objects) can be created from.
For example, a Year can be viewed as an abstract 
term (a class), while 2021 as a concrete year 
(an object).

SWARMBJECT classes has to be in ".scf" files,
and the name of the file (before the ".scf")
has to be the same as the class name.

A class is specified as:

```
/*In ClassName.scf*/
class ClassName {
	/*Members of the class.*/
}
```

The SWARMBJECT compiler ignores any class that 
is unused in the application to make compiling 
faster and the compiled code smaller.

Note: This also means that no error checking will 
be done on unused classes.

## Class members:

Classes can have data members and member functions.
Data members are to store data, while member 
functions implement some functionality. As a class
is abstract, its data members have no value, but in
the objects created from it each does have a value
individually. Similarly, member functions operate
on the object, not on the class.

A data member is specified as:

```
type name;
```

A member function is specified as:

```
type name(parameters){
 /*Code of the function.*/
}
```

Parameters each have a type and a name,
and are comma separated.

Member functions are called to execute their
functionality with their name and the arguments 
to use as the parameters in the function as:

```
name(arguments)
```

When called, a member function returns a value of the 
specified type. If it does not return any, then
the type is "void".

As an example let's create a "Year" class with a
numeric value as its data member, and functions 
to get the previous year, and to decrease it with 
some amount.

```
/*In Year.scf*/
class Year {
	int value;
	
	int getPrevious(){
		return value - 1;
	}
	
	void decrease(int amount){
		value = value - amount;
	}
}
```

The "getPrevious" function returns an "int" 
value, while the "decrease" function with the 
amount parameter does not return a value, hence 
the "void". Now let's create a "year" object, and 
call its functions.

```
/*In some function:*/
Year year;
/*Its members are accessed using the . operator.*/
year.value = 2021;
int previous = year.getPrevious();
/*"previous" is now 2020. */
year.decrease(1);
/*"year.value" is now also 2020. */
```

Note: The parameters of a function member receives 
only the value of the arguments, and gives back only 
the value of a returned construct. When access to 
the constructs themself are also needed, then 
pointers can be used, however it is the programmers 
duty to make sure that these constructs still exist,
when accessed through a pointer. As a class can 
be complex, functions members can not have class 
typed parameters, or return them, instead the same 
way pointers can be used.

When an object is created, its data members have
unspecified initial values, thus it is unsafe to 
access the values until some specific value gets 
assigned to the data members.

Similar to unused classes, the SWARMBJECT compiler 
ignores any member that is unused in a class, 
and it can also reorder the data members to 
minimize the size of the object, thus class 
members have no specified order.

The names of the class members are unique, 
thus two members within the same class can not 
have the same name.

## async classes:

A class is specified as async when there is an 
"async" keyword before the "class" keyword,
otherwise the class is non-async.

While non-async objects are created from non-async 
classes as a part of some other object or function,
async objects are created from async classes,
assigned to a thread, and can only be referenced.
Thus async objects are independent, with each async 
object being able to access only their own data 
members and member functions. However async objects 
can also have async functions, accessable even from 
other async objects.

A function is specified as async when there is an 
"async" keyword before its type, otherwise the 
function is non-async. Async functions can have 
only the "void" type.

Calling a non-async function is executed before 
the callee continues, while calling an async 
function the callee continues without waiting for 
the async function, as that is put to be executed 
in the object's thread. The advantage of threads 
is that while each of them can execute only one 
function at a time, but multiple threads can run at 
the same time, if the computer's resources allow it.

A reference to an async object is specified as:

```
AsyncClass aexcl/aptr referenceName 
```

After the async class's name, whose objects the 
reference can point to, the type of access is 
specified that this reference provides. The 
"aexcl" specifier means async exclusive access, 
that allows to access the data members and member 
functions. As async objects can access only 
their own data, it can point only to the async 
object whose async function is currently executed 
in the thread. The "aptr" specifier means a simple
async pointer, that allows to access only the 
async functions, thus it is usable between objects.
A data member can be "aptr" but not "aexcl".

An async function, can not have pointer parameters, 
except for async object references, as they could 
point to data not accessable to other objects, that 
the async function can be called with.

## Constructor and destructor 

A class can have a constructor function, that is 
automatically executed when an object is created.
It is useful as it can be used to initialize the 
data members to some default value.

A constructor is specified as a function with 
the same name as the class, and without a type:

```
ClassName(){

}
```

As an example let's create a "Year" class that
has an initial 2021 value.

```
/*In Year.scf*/
class Year {
	int value;
	
	Year(){
		value = 2021;
	}
}

/*In some function:*/
Year year;
/*"year.value" is 2021. */
```

If a class has data members with a class type also 
having a constructor, when an object is created, 
the constructor of the data members are called,
before the constructor of their containing class.
This way these data members are already initialized,
and thus usable, when the constructor is called.

A class can also have a destructor function, that is 
automatically executed when an object is destroyed.
An object is automatically destroyed, if it is a 
data member of some other object, that is destroyed,
or at the end of its containing block (between "{"
and "}"). It is useful as for example it might 
point to some object that has to know that this 
object will no longer point to it, and that can 
be done in the destructor.

A destructor is specified like a constructor,
but starting with a "~":

```
~ClassName(){

}
```

If a class has data members with a class type also 
having a destructor, when an object is destroyed,
the destructor of the data members are called,
after the destructor of their containing class.
This way these data members are still usable, 
when the destructor is called.

## constexpr data members:

Sometimes it is useful to assign a name to 
constant (unchanging) values, and use that name 
instead of the value, to make the code easier
to read. As these values are already known and 
unchangable in the application, accessing them 
are safe from any object.

A constexpr data member serves this purpose, as 
the compiler threats these as if just the value 
would have been written there instead of the name.
Thus these can be viewed as named literals.

A constexpr data member is specified as:

```
type constexpr name = value;
```

Accessing it is with:

```
Class::ConstexprMember 
/*Or if within the same class:*/
ConstexprMember 
```

As an example let's change the "Year" class 
to name the initial value.

```
/*In Constants.scf*/
class Constants {
	int constexpr initialYear = 2021;
}

/*In Year.scf*/
class Year {
	int value;
	
	Year(){
		value = Constants::initialYear;
	}
}
```

The value of a constexpr can even be computed,
like for example:

```
/*In Constants.scf*/
class Constants {
	int constexpr initialYear = 2021;
	int constexpr previousYear =
		initialYear - 1;
	/*previousYear is 2020*/
}
```

## enum classes:

An enum is a class, that has only constexpr data 
members, each automatically assigned an enumerated 
value in the order of their declaration as
0, 1, 2, ..., with the syntax:

```
enum ClassName {
	/*Comma separated member names.*/
}
```

As an example let's create a "RatedYear" class 
to rate how busy we were in a year.

```
/*In Rate.scf*/
enum Rate {
	low,    /*0*/
	medium, /*1*/
	high    /*2*/
}

/*In RatedYear.scf*/
class RatedYear {
	int value;
	unsigned char rate;
}

/*In some function:*/
RatedYear year;
year.value = 2021;
year.rate = Rate::high;
```

## Base classes:

When different classes share some common members, 
then these members can be separated into a base 
class, and any class using this base class will also 
have all the members of the base class.

A class using another class as its base is 
specified as:

```
/*In ClassName.scf*/
class ClassName : BaseClass {
	/*Additional members of the class,
		besides the members of the base.*/
}
```

As an example let's make the "RatedYear" class a 
base class of the "Year" class.

```
/*In Year.scf*/
class Year {
	int value;
}

/*In RatedYear.scf*/
class RatedYear : Year {
	unsigned char rate;
}

/*In some function:*/
RatedYear year;
year.value = 2021;
/*value is a member of the Year class, 
	but as it is a base class of RatedYear,
	it is also usable there.*/
```

## static data members:

Data members specified as static are like 
a constexpr, except that instead of being simply 
replaced with their value, they are stored in 
a designated area in the application, thus they 
can be pointed at, unlike a constexpr. However
if that is not needed, then a constexpr is 
more efficient.

A static data member is specified as:

```
type static name = value;
```

It is accessed the same way as a constexpr.

A string literal, while not being a data member 
of any class, but it is still a static data, as
it is already known, unchangable, and can be 
pointed at.

## static member functions:

Member functions called on an object have access 
to the object members, as these functions are 
associated with the object, through the "this" 
pointer. When this association is not needed, 
a member function can be specified as static. It
is useful, when only access to the function 
parameters are needed, as not having the object
association means less resource usage, and it also
allows to separate some functionalities outside to 
other classes.

A static member function is specified as:

```
static type name(parameters){
 /*Code of the function.*/
}
```

Note: The "static" keyword is before the type, 
as it is a specifier for the function, while with
data members it is after the type, as it is a 
specifier for the type.

It is accessed the same way as a static 
data member.

As an example let's put the "Year" class functions
to another class.

```
/*In Year.scf*/
class Year {
	int value;
}

/*In YearFunctions.scf*/
class YearFunctions {
	/*As these functions are now not automatically 
		associated with "Year" objects, the object
		has to be given to the function as a pointer.*/
		
	static int getPrevious(Year* year){
		/*Members through pointers are accessed using 
			the -> operator.*/
		return year->value - 1;
	}
	
	static void decrease(Year* year, int amount){
		year->value = year->value - amount;
	}
}

/*In some function:*/
Year year;
year.value = 2021;
int previous = YearFunctions::getPrevious(&year);
/*"previous" is now 2020. */
YearFunctions::decrease(&year, 1);
/*"year.value" is now also 2020. */
```

### Function pointers:

Function pointers are constructs that can point 
to static member functions with the specified 
return and parameter types. A function pointer 
that does not point anywhere has a nullptr value.

A function pointer type is specified as:

```
returnType(parameterTypes)
```

A function is called through a function pointer,
the same way as calling a function, but using 
the pointer's name instead of the function.

Let's call the previous example's "getPrevious" 
function indirectly through a function pointer.

```
/*In some function:*/
int(Year*) ptr = nullptr;
/*ptr can point to functions, returning an int, 
	and having a Year* parameter,
	but does not point anywhere so far.*/
Year year;
year.value = 2021;
ptr = YearFunctions::getPrevious;
/*ptr is set to point to the "getPrevious" 
	function.*/
int previous = ptr(&year);
/*"previous" is now 2020. */
```

## static async functions:

Like static non-async functions, static async 
functions are not automatically associated 
with the class objects, thus they can access 
only the parameters. If it has an "aexcl" 
parameter, then calling the function puts it to 
be executed in that object's thread, in order to 
be able to access the members of that parameter,
however if it has an no "aexcl" parameter, then 
calling the function just puts it to be executed 
in the current thread.

A static async function is specified as:

```
static async void name(parameters){
 /*Code of the function.*/
}
```

# Statements, expressions, operators.

The code of the functions consists of statements, 
with expressions, using operators.

## block statement:

A block statement is used to contain a sequence 
of statements.

```
{
	/*Statements.*/
}
```
	
## variable declaration:

```
/*With unspecified initial value,
	or using the class constructor.*/
type name;
/*With specified initial value,
	if not a class type.*/
type name = expression;
```

A variable is a named data containing construct.
available starting from its declaration,
until the end of its containing block.

```
{
	/*"year" is created here:*/
	Year year;
	/*"year" is destroyed here.*/
}
/*"year" is not available here.*/
```

## return statement:

```
/*Returning without a value:*/
return;
/*Returning with a value:*/
return expression;
```

Ends the function execution with or without 
giving back some value. The value has to be of
the same type as the function's return type, or
no value if the type is "void". Any already 
declared variables of its containing blocks are 
destroyed, and further statements of the function 
are not executed.

```
/*In some class:*/
static int getYear(){
	return 2021;
	return 2020;
}

/*In some function of the same class:*/
int year = getYear();
/*"year" is 2021. */
```

## if statement:

```
if (expression){
	/*Statements.*/
} else if (expression){
	/*Statements.*/
/*More else ifs.*/
} else {
	/*Statements.*/
}
```

When the "if" expression is true, its block 
is executed, but if it is false, then the 
first "else if" that is true is executed, or if
all are false, then the "else" block is executed.
The "else if" and the "else" parts can be omited 
if not needed.

Let's create a function that converts a 
rate value to a string.

```
/*In some class:*/
static unsigned char const[]
	rateToString(unsigned char rate){
	unsigned char const[] string;
	/* "==" checks if the operands are equal. */
	if (rate == Rate::low){
		string = "low";
	} else if (rate == Rate::medium){
		string = "medium";
	} else {
		string = "high";
	}
	return string;
}
```

## while statement:

```
while (expression){
	/*Statements.*/
}
```

When the "while" expression is true, its block 
is executed, then the expression is checked again, 
whether to execute the block again, etc. Thus 
the block is executed repeatedly, as long as the 
expression is true.

Let's execute some code 2021 times:

```
unsigned short i = 0;
while (i < 2021){
	/*Some code.*/
	i = i + 1;
}
```

## break statement:

```
break;
```

Sometimes it is useful to break out of a while 
statement before its expression becomes false.
A break statement does this by immediately 
stopping the execution of its closest containing 
while statement, and destroying any of its already 
declared variables.

Let's complicate the while statement example 
by using a break statement:

```
unsigned short i = 0;
while (true){
	if (i == 2021) {break;}
	/*Some code.*/
	i = i + 1;
}
```

## continue statement:

```
continue;
```

A continue statement acts as if the while 
block's end would have been reached, thus 
instead of executing any of its further 
statements, the while expression is checked 
whether to execute the block again.

Let's complicate the while statement example
even further by using a continue statement:

```
unsigned short i = 0;
while (true){
	if (i < 2021){
		/*Some code.*/
		i = i + 1;
		continue;
	}
	break;
}
```

## switch statement:

```
switch (expression){
	case value:
		/*Statements.*/
	/*More cases.*/
	default:
		/*Statements.*/
}
```

When having to decide between a set of individual 
values, using else ifs are not efficient, as each 
expression has to be checked in sequence, until
the correct one is found. Instead a switch 
statement jumps to the "case" label with the same 
value as the switch's expression, or if there is 
no such label, then to the "default" label, if 
provided. After the jump, all further statements 
are executed, until a break statement or the end 
of the switch block, thus even statements of the 
further labels.

Let's rewrite the if statement example
by using a switch statement:

```
/*In some class:*/
static unsigned char const[]
	rateToString(unsigned char rate){
	unsigned char const[] string;
	switch (rate){
		case Rate::low :
			string = "low";
			break;
		case Rate::medium :
			string = "medium";
			break;
		default:
			string = "high";
	}
	return string;
}
```

## constwrite statement:

```
constwrite "code";
```

A constwrite statement is intended only for 
developers, having to write platform dependent 
code, as it simply compiles the operand as 
unprocessed code.

## constif statement:

When the "constif" expression is true, then the 
statements of its block are compiled, but if 
it is false, then it is ignored as if it were 
just like a comment, and the first "else if" 
that is true is compiled, or if all are false, 
then the "else" block is compiled. The "else if" 
and the "else" parts can be omited if not needed.

```
bool constexpr compile = true;

/*In some function:*/
constif (compile){
	/*This block is compiled. */
} else {
	/*This block is ignored. */
}
```

## consterror statement:

Stops the compiler and logs a 
string literal as an error.

```
/*In some function:*/
constif (compile){
	consterror "error";
}
```

## Expressions:

The simplest expressions are the use of literals, 
data members, member functions, parameters, 
variables and function calls. More complex 
expressions consist of operators and their 
operands. Operators are unary or binary as
they have 1 or 2 operands.

## Binary = operator:

The assignment operator is used to assign a 
value to a data holding construct.

```
int year = 2021;
```

## Unary + operator:

The plus operator is used to create a 
positive number.

```
int year = +2021;
```

## Unary - operator:

The minus operator is used to create a 
negative number.

```
int year = -2021;
```

## Binary + operator:

The addition operator is used to 
add numbers.

```
int year = 2020 + 1; /*2021*/
```

## Binary - operator:

The substraction operator is used to 
substract numbers.

```
int year = 2021 - 1; /*2020*/
```

## Binary * operator:

The multiplication operator is used to 
multiplicate numbers.

```
int year = 2021 * 2; /*4042*/
```

## Binary / operator:

The division operator is used to 
divide numbers.

```
int year = 4042 / 2; /*2021*/
```

## Binary % operator:

The modulus operator is used to get 
the remainder of a division.

```
unsigned char years = 4042 % 2; /*0*/
```

## Unary ! operator:

The logical negation operator is used to 
change a true value to a false value, 
and a false value to a true value.

```
bool check = !true; /*false*/
```

## Binary && operator:

The logical and operator is used to 
create a true value if both operands 
are true, or false otherwise.

```
bool check = true && false; /*false*/
```

## Binary || operator:

The logical or operator is used to 
create a false value if both operands 
are false, or true otherwise.

```
bool check = true || false; /*true*/
```

## Binary < operator:

The less than operator is used to create a 
true value if the first numeric operand is 
less than the second, or false otherwise.

```
bool check = 2020 < 2021; /*true*/
```

## Binary > operator:

The greater than operator is used to create a 
true value if the first numeric operand is 
greater than the second, or false otherwise.

```
bool check = 2020 > 2021; /*false*/
```

## Binary <= operator:

The less than or equal operator is used 
to create a true value if the first numeric 
operand is less than or equal to the second, 
or false otherwise.
```
bool check = 2020 <= 2021; /*true*/
```

## Binary >= operator:

The greater than or equal operator is used 
to create a true value if the first numeric 
operand is greater than or equal to the 
second, or false otherwise.

```
bool check = 2020 >= 2021; /*false*/
```

## Binary == operator:

The equal to operator is used to create a 
true value if the first operand has the 
same value as the second, or false otherwise.

```
bool check = 2020 == 2021; /*false*/
```

## Binary != operator:

The not equal to operator is used to create a 
true value if the first operand does not have 
the same value as the second, or false otherwise.

```
bool check = 2020 != 2021; /*true*/
```

## Unary ~ operator:

The bitwise complement operator is used to 
change in a binary integer the 0 digits to 1, 
and the 1 digits to 0.

```
unsigned int year =
	~0b11111100101;
	/* 00000011010 */
```

## Binary & operator:

The bitwise and operator is used to create a 
binary integer containing 1 digits where both 
operands has a 1 digit, and 0 digits elsewhere.

```
unsigned int year =
	0b011111100101 &
	0b111111001010;
	/*011111000000*/
```

## Binary | operator:

The bitwise inclusive or operator is used to 
create a binary integer containing 1 digits 
where either operands has a 1 digit, and 
0 digits elsewhere.

```
unsigned int year =
	0b011111100101 |
	0b111111001010;
	/*111111101111*/
```

## Binary ^ operator:

The bitwise exclusive or operator is used to 
create a binary integer containing 0 digits 
where both operands has the same digit, and 
1 digits elsewhere.

```
unsigned int year =
	0b011111100101 ^
	0b111111001010;
	/*100000101111*/
```

## Binary << operator:

The left shift operator is used to shift 
the digits of a binary integer left by 
the value of the second operand.

```
unsigned int year =
	 0b11111100101 << 1;
	/*111111001010*/
```

## Binary >> operator:

The right shift operator is used to shift 
the digits of a binary integer right by 
the value of the second operand.

```
unsigned int year =
	0b111111001010 >> 1;
	/* 11111100101 */
```

## Unary & operator:

The address of operator is used to create a 
pointer to a data holding construct.

```
int year;
int* ptr = &year;
```

## Unary * operator:

The indirection operator is used to 
reference what a pointer is pointing to.

```
int year;
int* ptr = &year;
*ptr = 2021;
```

## Binary . operator:

The member operator is used to directly 
access an object member.

```
Year year;
year.value = 2021;
```

## Binary -> operator:
	
The member pointer operator is used to indirectly 
access an object member through a pointer.

```
Year year;
Year* ptr = &year;
ptr->value = 2021;
```

## new operator:

Storing data in data members and variables are 
efficient when they are expected to be used in the 
application. However it is often not possible to 
know if a construct will be needed or not, like
when it depends on the user's interaction with 
the application. To solve this, constructs can 
also be created dynamically using the new operator.
While less efficient, but can be used to create 
constructs only when needed.

```
/*Dynamically created type.*/
new type

/*Dynamically created array.*/
new type[size]

/*Dynamically created async object.*/
new(instance, thread) asyncClass 
```

The new operator returns a pointer to the 
created construct.

```
Year* year = new Year;
year->value = 2021;
```

Async objects can only be created dynamically.
If both the instance and thread arguments are 
ommited, then the async object is created in a 
random instance's random thread. Otherwise the 
instance argument has to be an async object, 
and the object is created in the same instance 
as the argument's. The thread argument can be 
ommited to create the object in a random 
thread, -1 to create the object in the same 
thread as the instance argument's, and >=0 to 
create the object in the given thread index.

## delete operator:

Dynamically created constructs are not destroyed 
automatically at the end of the block that they 
were created in, to be able to keep using them, as 
long as needed. Instead it is the programmer's 
duty to destroy them with the delete operator when 
not needed anymore.

```
/*Delete dynamically created type.*/
delete pointer;

/*Delete dynamically created array.*/
delete[] arrayPointer;

/*Delete current async object.*/
delete;
```

The construct pointed by the statement's operand 
is deleted.

```
Year* year = new Year;
/*When not needed anymore:*/
delete year;
```

When deleting an array, the delete[] statement 
is used instead.

Async objects can not be deleted using the pointer 
syntax, as they can be referenced from other 
async objects, and deleting them through such 
pointers would not mean immediate deletion.
Instead the delete statement can be used without an 
operand in an async function. The function 
execution is ended, thus further statements of 
the function are not executed, and the async object 
associated with the function is deleted immediately.
This information is propaganated through the 
instances, automatically setting any reference to 
the object to nullptr. Further calling any of its 
async functions are ignored.

## [] operator:

The subscript operator is used to access the 
indexed element of an array pointer. The 
indexing starts with 0.

```
int[] years = new int[2];
years[0] = 2020;
years[1] = 2021;
/*When not needed anymore:*/
delete[] years;
```

## Type casting:

```
(type)expression 
```

Type casting allows converting between compatible 
numeric types or pointers, as the expression is 
converted to the given type.

When arithmetic operators are used with numeric 
constructs, if both operands are of the same type, 
that will be the type of the result too. For 
example, adding chars results a char. If the 
operands only differ as signed and unsigned, 
then the result will have the signed type. For 
example, adding a char and an unsigned char 
results a char. If one of the operands has a 
greater range than the other, then the result 
will have the greater type. For example, adding 
a char and an int results an int. These rules 
are to support common usage, however sometimes 
a different type is needed, allowed by type casting.

```
unsigned char year = 21;
unsigned char previous = 20;
char result = (char)previous - year;
/*Without casting, the result would have to be 
	unsigned char, however -1 is a negative number.*/
```

Note: As types were defined as at least, the 
example might have a correct result even without 
the casting, however such usage is unsafe.

During assignment, a pointer type can be 
automatically converted to a base type or to a 
void* type, as that can point to any type. Only
the base members are accessable through a base 
converted pointer, while the construct is not 
accessable at all through a void* type. It can
however be converted back by casting.

```
Year* year = new RatedYear;
/*The construct is actually a "RatedYear", but 
pointed as a "Year".*/
year->value = 2021;
/*The base "value" is accessable.*/
(RatedYear*)year->rate = Rate::high;
/*The "rate" member is accessable only if casted.*/
void* ptr = year;
(RatedYear*)ptr->value = 2020;
/*Through the "ptr", even the "value" member 
	is accessable only after casted.*/
```

Note: The original type of a down converted 
pointer is not known automatically, thus it is 
the programmer's duty to cast it to the correct 
type. Likewise deletion should not be made 
through a down converted pointer, as then the 
destructor of the original type and its 
additional members are not executed.

## Parenthesized expressions:

To change what is considered as the operand 
of an operator, it can be parenthesized.

```
(unsigned int)(year->value)
/*Converts the "value", instead of the "year".*/
```

# Standard (std) reference:

* [/docs/std/ApplicationInstance.md](std/ApplicationInstance.md)
* [/docs/std/NumberBases.md](std/NumberBases.md)

## Array (arr) reference:

* [/docs/std/arr/Char.md](std/arr/Char.md)
* [/docs/std/arr/Float.md](std/arr/Float.md)
* [/docs/std/arr/Int.md](std/arr/Int.md)
* [/docs/std/arr/Ptr.md](std/arr/Ptr.md)
* [/docs/std/arr/Short.md](std/arr/Short.md)
* [/docs/std/arr/Uchar.md](std/arr/Uchar.md)
* [/docs/std/arr/Uint.md](std/arr/Uint.md)
* [/docs/std/arr/Ushort.md](std/arr/Ushort.md)
* [/docs/std/arr/Void.md](std/arr/Void.md)

## BOM (bom) reference:

* [/docs/std/bom/Window.md](std/bom/Window.md)

## Compile (cmpl) reference:

* [/docs/std/color/Default.md](std/color/Default.md)
* [/docs/std/color/Platforms.md](std/color/Platforms.md)
* [/docs/std/color/Verbosity.md](std/color/Verbosity.md)

## Color (color) reference:

* [/docs/std/color/RGB.md](std/color/RGB.md)

## CSS (css) reference:

* [/docs/std/css/AlignTypes.md](std/css/AlignTypes.md)
* [/docs/std/css/BorderStyles.md](std/css/BorderStyles.md)
* [/docs/std/css/Declaration.md](std/css/Declaration.md)
* [/docs/std/css/DisplayTypes.md](std/css/DisplayTypes.md)
* [/docs/std/css/Keyword.md](std/css/Keyword.md)
* [/docs/std/css/MarginTypes.md](std/css/MarginTypes.md)
* [/docs/std/css/OverflowTypes.md](std/css/OverflowTypes.md)
* [/docs/std/css/RGB.md](std/css/RGB.md)
* [/docs/std/css/Short.md](std/css/Short.md)
* [/docs/std/css/TextAlignTypes.md](std/css/TextAlignTypes.md)
* [/docs/std/css/Units.md](std/css/Units.md)
* [/docs/std/css/Value.md](std/css/Value.md)
* [/docs/std/css/ValueTypes.md](std/css/ValueTypes.md)
* [/docs/std/css/WhiteSpaceTypes.md](std/css/WhiteSpaceTypes.md)

## Data structures (ds) reference:

* [/docs/std/ds/Array.md](std/ds/Array.md)
* [/docs/std/ds/BalBinTree.md](std/ds/BalBinTree.md)
* [/docs/std/ds/BinTree.md](std/ds/BinTree.md)
* [/docs/std/ds/Buffer.md](std/ds/Buffer.md)
* [/docs/std/ds/CircuralArray.md](std/ds/CircuralArray.md)
* [/docs/std/ds/DArray.md](std/ds/DArray.md)
* [/docs/std/ds/DBuffer.md](std/ds/DBuffer.md)
* [/docs/std/ds/DLList.md](std/ds/DLList.md)
* [/docs/std/ds/PtrArray.md](std/ds/PtrArray.md)
* [/docs/std/ds/PtrCircuralArray.md](std/ds/PtrCircuralArray.md)
* [/docs/std/ds/PtrDArray.md](std/ds/PtrDArray.md)
* [/docs/std/ds/SLList.md](std/ds/SLList.md)

## DOM (dom) reference:

* [/docs/std/dom/CharacterData.md](std/dom/CharacterData.md)
* [/docs/std/dom/ClipboardEvent.md](std/dom/ClipboardEvent.md)
* [/docs/std/dom/Element.md](std/dom/Element.md)
* [/docs/std/dom/Event.md](std/dom/Event.md)
* [/docs/std/dom/KeyboardEvent.md](std/dom/KeyboardEvent.md)
* [/docs/std/dom/MouseEvent.md](std/dom/MouseEvent.md)
* [/docs/std/dom/Node.md](std/dom/Node.md)
* [/docs/std/dom/NodeTypes.md](std/dom/NodeTypes.md)
* [/docs/std/dom/Range.md](std/dom/Range.md)
* [/docs/std/dom/Selection.md](std/dom/Selection.md)
* [/docs/std/dom/Text.md](std/dom/Text.md)

## File system (fs) reference:

* [/docs/std/fs/EntryTypes.md](std/fs/EntryTypes.md)
* [/docs/std/fs/File.md](std/fs/File.md)
* [/docs/std/fs/FileSystem.md](std/fs/FileSystem.md)
* [/docs/std/fs/Folder.md](std/fs/Folder.md)
* [/docs/std/fs/GUI.md](std/fs/GUI.md)
* [/docs/std/fs/OpenFileModes.md](std/fs/OpenFileModes.md)

## HTML (html) reference:

* [/docs/std/html/AElement.md](std/html/AElement.md)
* [/docs/std/html/BrElement.md](std/html/BrElement.md)
* [/docs/std/html/DivElement.md](std/html/DivElement.md)
* [/docs/std/html/Document.md](std/html/Document.md)
* [/docs/std/html/Element.md](std/html/Element.md)
* [/docs/std/html/InputElement.md](std/html/InputElement.md)
* [/docs/std/html/InputTypes.md](std/html/InputTypes.md)
* [/docs/std/html/PreElement.md](std/html/PreElement.md)

## String (str) reference:

* [/docs/std/str/Compare.md](std/str/Compare.md)
* [/docs/std/str/CString.md](std/str/CString.md)
* [/docs/std/str/DString.md](std/str/DString.md)
* [/docs/std/str/String.md](std/str/String.md)
* [/docs/std/str/View.md](std/str/View.md)

## Value (val) reference:

* [/docs/std/val/Char.md](std/val/Char.md)
* [/docs/std/val/Float.md](std/val/Float.md)
* [/docs/std/val/Int.md](std/val/Int.md)
* [/docs/std/val/Ptr.md](std/val/Ptr.md)
* [/docs/std/val/Short.md](std/val/Short.md)
* [/docs/std/val/Uchar.md](std/val/Uchar.md)
* [/docs/std/val/Uint.md](std/val/Uint.md)
* [/docs/std/val/Ushort.md](std/val/Ushort.md)

# Software license

Copyright (c) 2021-2023 SWARMBJECT contributors

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

Copyright (c) 2021-2023 SWARMBJECT contributors

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