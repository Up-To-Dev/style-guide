# Code style guide

Created: Jan 1, 2021 9:42 PM
Created By: Ben Goodwin
Last Edited By: Ben Goodwin
Last Edited Time: Jan 2, 2021 10:07 PM

# General Guide

### Spacing

- Use spaces, not tabs. Tabs should only appear when they are needed for semantic meaning, for example in makefiles. The indent size is 4 spaces (note almost all editors allow for a tab key to correspond to 4 space).
- Do not place spaces around unary operators, but place spaces around binary and ternary operators.

```jsx
//right 
i++

//wrong
i ++

//right
y = m * x + b;
f(a, b);
c = a | b;
return condition ? 1 : 0;

//wrong
y=m*x+b;
f(a,b);
c = a|b;
return condition ? 1:0;
```

- Do not place spaces between control statements and their parenthesis

```jsx
//right 
if(x>y){
	doIt();
}

//wrong
if (x>y) {
	doIt();
}
```

- Each statement should have its own line

```jsx
//right
x++;
y++;

//wrong
x++; y++;
```

### Bracing

I know this is somewhat a point of contention, but for function definitions, place each brace on its own line, and for other braces, control statements for example, place the open brace on the line preceding the code block; place the closing brace on its own line.

```jsx
//right 

int main()
{
  ...
}

for (int i = 0; i < 10; ++i) {
    ...
}

//wrong

int main(){
  ...
}

for (int i = 0; i < 10; ++i) 
{
    ...
}

```

- One-line control clauses should not use braces unless comments or needed or a reasonable line length is exceeded.

### Comments

- Use one space before the body of the comment and in-between sentences in comments.
- Try to use correct grammar where possible.

### Source File Basics

- File names must be all lowercase (with the exception of vue components and pages) and may include underscores or dashes, but no additional punctuation. Follow the convention that the project/repo uses.
- All source code files are encoded in UTF-8

### General Naming Conventions

Identifiers use only ASCII letters and digits, and in a small number of cases noted below, underscores and very rarely (when required by languages or frameworks) dollar signs.

- Give as descriptive a name as possible, within reason. Do not worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader. Do not used abbreviation that are ambiguous or unfamiliar to readers outside the project, so not abbreviate by deleting letters within a word.
- Generally use camelCase

```jsx
//Good Examples

errorCount 
dnsConnectionIndex // Most people know what "DNS" stands for.
referrerUrl // Likewise for URL.
customerId // Id is clear and unlikely to be misunderstood.

// Bad Examples

n // meaningless
nErr // Ambiguous abbreviation
nCompConns // Ambiguous abbreviation
wcgConnections // Not clear to outsiders
pcReader // Lots of things can be abbreviated to 'pc'
cstmrID // Deletes internal letters
```

### Rules by identifier type

- Package names: Package names are all lowerCamelCase.
- Class names: Class, interface, record and typedef names are written in UpperCamelCase. Unexpected classes are simply locals; They are not marked "@private" and therefore are not named with a trailing underscore.
- Method names: Method names are written in lowerCamelCase. Names for "@private" methods must end with a trailing underscore.
- Enum names: Enum names are written in UpperCamelCase, similar to classes, and should generally be singular nouns. Individual items within the enum are named in "CONSTANT_CASE".
- Constant names: Constant names use "CONSTANT_CASE" : all uppercase letters, with words separated by underscores. There is no reason to use a trailing underscore, since private static properties can be replaced by (implicitly private) module locals.
- Non-constant field names: Non-constant field names (static or otherwise) are written in lowerCamelCase, with a trailing underscore for private fields
- Parameter names: Parameter names are written in lowerCamelCase. Even if the parameter expects a constructor
- Local variable names: Local variable names are written in lowerCamelCase, except for module-local (top level) constants, as described above.
- Template parameter names: Template parameter names should be concise, single word or single-letter identifiers, and must be all caps such as "THIS" or "TYPE"
- Module-local names: Module-local names that are not exported are implicitly private. They are not marked "@private" and do not end in an underscore. This applies to classes, functions, variables, constants, enums, and other module-local identifiers.

# HTML / CSS

Ensure valid HTML where possible. Use valid HTML code unless that is not possible due to otherwise unattainable performance goals regarding file size.

Use tools such as the W3C HTML validator to test.

Using valid HTML is a measurable baseline quality attribute that contributes to learning about technical requirements and constraints, and that ensures proper HTML usage.

### Protocol

- Use HTTPS for embedded resources where possible.
- Always use HTTPS for images and other media files, style sheets, and scripts, unless the respective files are not available over HTTPS.

### General Formatting Rules

- Capitalisation
    - Use only lowercase. All our HTML code must be lowercase. This applies to HTML element names, attributes, attribute values, CSS selectors, properties, and property values (with the exception of strings).
- Remove trailing whitespace
    - trailing white spaces are unnecessary and can complicate diffs.

### General Meta Rules

- Encoding: Use UTF-8 (no BOM). Make sure your editor uses UTF-8 as character encoding, without a byte order mark. Specify the encoding in HTML templates and documents via "<meta charset="utf-8">". Do not specify the encoding of style sheets as these assume UTF-8.
- Comments: Explain code as needed, where possible. Use comments to explain code; What does it cover, what purpose does it serve, why is respective solution used or preferred?

# JAVASCRIPT

## ES Modules

### Imports

- Import statements must not be line-wrapped and are therefore an exception to the 80 column limit.
- File extensions in import paths are not optional and must always be included.

```jsx
//Like so... 
import * as parent from '../parent.js';
```

- Do not import the same file multiple times. This can make it hard to determine the aggregate imports of a file.
- Name imports using camelCase and use names derived from the imported file name.
- Default import names are derived from the imported file name as follows

```jsx
import MyClass from '../my-class.js';
import myFunction from '../my_function.js';
import SOME_CONSTANT from '../someconstant.js';
```

### Column Limit: 80

JavaScript code has a column limit of 80 characters. Except as noted below, any line that would exceed this limit must be line-wrapped.

1. ES module "import" and "export from" statements
2. Lines where obeying the column limits is not possible or would hinder discoverability. for example;
    - A long URL which should be clickable in the source code
    - A shell command intended to be copied and pasted
    - A long string literal which may need to be copied or searched for in its entirety (e.g, a long file path).

### Whitespace

Aside from the line terminator sequence, the ASCII horizontal space character (0x20) is the only whitespace character that appears anywhere in the source file. This implies that

1. All other whitespace characters in string literals are escaped, and 
2. Tab characters are not used for indentation.

## Language Features

Javascript includes many dubious (potentially dangerous) language features. This section delineates which features may or may not be used, and any additional constraints on their use.

### Local Variable declarations

- Use "const" and "let"
    - Declare all local variables with either "const" or "let". Use "const" by default unless a variable needs to be reassigned. The "var" keyword must not be used.
- One variable per declaration
    - Every local variable declaration declares only one variable. "let a = 1, b=2;" is not allowed.
- Declared when needed, initialised as soon as possible.
    - Local variables are not habitually declared at the start of their containing block or block-like structure. Instead, local variables are declared close to the point they are first used.

### Array literals

- Use trailing commas
    - Include a trailing comma whenever there is a line break between the final element and the closing bracket

    ```jsx
    const values = [
      'first value',
      'second value',
    ];
    ```

### Object literals

- Use trailing commas
    - include a trailing comma whenever there is a line break between the final property and closing brace.
- Do not use the "Object" constructor
    - While "Object" does not have the same problems as "Array" it is disallowed for consistency. Use and object literal instead ( {} or {a:0, b:1 })
- Do not mix quoted and unquoted keys
    - Object literals may represent either structs (with unquoted keys and/or symbols) or dicts (with quoted and/or computed keys). Do not mix these key types in a single object literal.

    ```jsx
    // Disallowed
    {
      width: 42, // struct-style unquoted key
      'maxWidth': 43, // dict-style quoted key
    }
    ```

    ### Classes

    - Constructors: constructors are optional. Subclass constructors must call "super()" before setting any fields or otherwise accessing "this". Interfaces should declare non-method properties in the constructor.
    - Fields: Set all of a concrete object's fields (i.e. all properties other than methods) in the constructor. Annotate fields that are never reassigned with "@const" (these do not need to be deeply immutable). Annotate noon-public fields with the proper visibility annotation ("@private", "@protected", "@package"), and end all "@private" fields' names with an underscore. Fields are never set on a concrete class "prototype".

    ```jsx
    // Example

    class Foo {
      constructor() {
        /** @private @const {!Bar} */
        this.bar_ = computeBar();

        /** @protected @const {!Baz} */
        this.baz = computeBaz();
      }
    }
    ```

    ### Functions

    - Top-level functions
        - Top-level function may be defined directly on the "exports" object, or else declared locally and optionally exported

        ```jsx
        // Examples

        /** @param {string} str */
        exports.processString = (str) => {
          // Process the string.
        };

        /** @param {string} str */
        const processString = (str) => {
          // Process the string.
        };

        exports = {processString};
        ```

- Nested functions and closures
    - functions may need to contain nested function definitions. If it is useful to give the function a name it should be assigned to a local "const".
- Arrow functions
    - Arrow functions provide a concise function syntax and simplify scoping "this" for nested functions. Prefer arrow functions over the "function" keyword. particularly for nested functions.
    - The left-hand side of the arrow contains zero or more parameters. Parentheses around the parameters are optional if there is only a single non-destructured parameter. When parentheses are used, inline parameter types may be specified.

### String Literals

- Use single quotes: Ordinary string literals are delimited with single quotes ('), rather than double quotes (").

Tip: if a string contains a single quote character, consider using a template string to avoid having to escape the quote.

- Ordinary string literals may not span multiple lines.

### Exceptions

Exceptions are an important part of the language and should be used whenever exceptional cases occur. Always throw "Error"s or subclasses of "Error": never throw string literals or other objects. Always use "new" when constructing an "Error".

- Ensure you do not give any excess information or system details away in the error message.

# VUE

The core team is adopting Vue as a new technology so it is to be expected that this section will change as we become more experienced with the framework. For now we have some basic standards to operate ensure readability and that we are all on the same page.

Follow the offical Vue documentation style guide where possible ([https://vuejs.org/v2/style-guide/](https://vuejs.org/v2/style-guide/)).

# PYTHON

For python use PEP8 style. ([https://pep8.org/](https://pep8.org/))

### Unspecified Issues

Just be consistent! If you are unsure about formatting or an issue that is not covered in the style guide just stay consistent, and be considerate of others who may have to work on the code in the future.  

If you’re editing code, take a few minutes to look at the code around you and determine its style. If they use spaces around all their arithmetic operators, you should too. If their comments have little boxes of hash marks around them, make your comments have little boxes of hash marks around them too.

## Final Comments

Although the style guide should be adhered to when possible, we are a very small team working to push an ambitious project, and style, although important, is not the be all and end all.  Commits will not be pulled up based on small style issues. We value all contributions and are focused on creating a fully user driven experience. That being said, don't make anything harder for the next developer than it needs to be.