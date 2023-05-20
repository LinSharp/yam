# Yam
## A simple human readable configuration language.

Yam is a tuber.

## Syntax

```
~~ Configuring display.
- <|time|>
- version:
    "0.1.2"
- background:
    svg: <load>background.svg</load>
    transparency: 60%
    color: 255|255|255
- !Display
    menu: <load>pages/index.html</load>
    options: <load>pages/options.html</load>
    log_path: logs/display.log
    settings:
      width: 1920
      height: 1080
      mode: fullscreen
    show_hidden: false
```

### Base Types

- Comments - Start with double tilde "\~\~". Everything after \~\~ will be ignored.  
    **Example:**  
    `~~ This is a comment`

- Number - Everything that starts with a digit or a dash "-" (for negative numbers)
    will be considered a number. There can't be a space between a dash and a number.
    If programming language distinguishes, number will be further split to integer
    and float/double. Float is a number with a decimal point.  
    **Examples:**  
    `123` is a number/integer  
    `-456` is a negative number/integer  
    `3.14` is a number/float  
    `-2.718` is a negative number/float  
    `50%` is converted to a number/float  
    `1/4` is  converted to a number/float  
    `0x1B13` is converted from hexadecimal to number  (unsupported for now)  
    `0b0001` is converted from binary to number  (unsupported for now)  

- Text - Everything that starts with a letter or a symbol, will be consigered as text.
    It is possible to make everything into text, if it's put in double quotes.
    To set text over multiple lines, put it inside tripple quotes. Multi line text
    has to be written in the same indent level. as the quotes. All characters from the indent
    towards base indent, will be removed.  
    **Example1:**  
    `"This is text. 3.14 is also considered as text"`  
    **Example2:**
    ```
    """
    This text
    is written
    over multiple
    lines
    """
    ```

- Boolean - A boolean is either `true` or `false`. Have to be lowercase.

- Hashtable/Dictionary - Dictionary consists of key, value pairs, where key is
    anything, that starts with a character and end in a column ":".
    Value can be any other type.  
    **Example1:**  
    ```
    key: value
    ```
    **Example2:**  
    ```
    outer_key:
      inner_key1:
        value1
      inner_key2:
        value2
    ```

- List - A list consists of items of any type. List items have to prepend
    a dash and space "- ". For listing items in a single line, seperate items with a bar "|".  
    **Example1:**
    ```
    - A
    - list
    - of
    --- inner
      - list
      - of
      - items
    - items
    ```
    **Example2:**
    ```
    A | list | of | items
    ```
    **Example3:**
    ```
    - A
    - list
    - of
    - inner | list | of | items
    - items
    ```

### Extended types

Extended types are types, that need references to a custom function or class for decoding.

- Object - An object is represented similary to dictionary. Base key that starts
    with an exclamation mark - "!". Inner dictionary key names will be
    considered as member variable names of the object. Unlike a dictionary base
    key does not end with a column - ":".  
    A reference to a class with the same name is needed. By default parser will
    search for a decode() method inside the class and pass variables to it,
    if it does not find it, it will use the variables to instantiate the class.  
    **Example:**
    ```
    !Object
      variable1: value1
      variable2: value2
      variable3: value3
    ```

- Tag - A tag is made by starting with `<tag_name>`, closing with `</tag_name>`,
    and putting content in the middle. Tags that do not need content can be
    done this way: `<|tag_name|>`  
    A reference to a function, that will decode the tag is needed. It can be
    passed as a keyword argument to the parser. The content within tag is passed
    to the decoding function as text.  
    **Example1:**
    ```
    <tag>Content</tag>
    ```
    **Example2:**
    ```
    <|tag|>
    ```
    **Default tags:**  
    Default tags will be replaced by custom ones with the same name.  
    **load:** \
    Loads file from path.  
    `<load>Path</load>`  
    **time:** \
    Formats ISO timestamp.  
    `<time>1991-08-22</time>`
    or
    `<time>24:59:59.999</time>`
    or
    `<time>1991-08-22T24:59:59.999</time>`  
    `<|time|>` - get current ISO time.


### File structure
In examples, each block is considered a file. Yam files have .yam extension.  
Base indent can contain either a list or a hashtable/dictionary, can't be mixed. Indent is 2 spaces.  

Base list:
```
- 3.14
- is
- roughly
- pi
```

Base dictionary:
```
Dozen:
  12
PI:
  3.14
Fruits:
  Apples:
    Tasty
  Pears:
    Okay
```
