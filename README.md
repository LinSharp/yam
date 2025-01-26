# Yam
A simple human writable, data oriented configuration language.  
Yam is a tuber.

## Syntax

```
~~ Configuring display.
- <time/>
- version:
    "0.1.2"
- background:
    svg: <l>background.svg</l>
    transparency: 60%
    color: !Color(255,255,255)
- !Display
    menu: <l|html>pages/index.html</l|html>
    options: <l>pages/options.html</l>
    log_path: logs/display.log
    settings:
      width: 1920
      height: 1080
      mode: fullscreen
    show_hidden: false
- style: <l>style.yam</l>
```

### Base Types

- Comments - Start with double tilde "\~\~". Everything on the line after \~\~ will be ignored.  
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

- Text - Everything that starts with a letter or a symbol, will be considered as text.
    It is possible to make everything into text, if it's put in double quotes.
    To set text over multiple lines, put it inside tripple quotes. Multi line text
    has to be written in the same indent level. as the quotes. All characters from the indent
    towards base indent, will be removed.  
    **Example 1:**  
    ```
    This is text. 
    "3.14 is also considered as text"  
    ```
    **Example 2:**
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
    **Example 1:**  
    ```
    key: value
    ```
    **Example 2:**  
    ```
    outer_key:
      inner_key1:
        value1
      inner_key2:
        value2
    ```

- List - A list consists of items of any type. List items have to prepend
    a dash and space "- ". For listing items in a single line, seperate items with a bar "|".  
    **Example 1:**
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

    **Example 2:**
    ```
    "John" | "Doe" | 21 | "13.4 €"
    ```

    **Example 3:**
    ```
    - A
    - list
    - of
    - "inner" | "list" | "of" | "items"
    - items
    
### Extended types

Extended types are types, that need references to a custom function or class for decoding.

- Object/Struct - An object is represented similary to dictionary. Base key that starts
    with an exclamation mark - "!". Inner dictionary key names will be
    considered as member variable names of the object. Unlike a dictionary, base
    key does not end with a column - ":".  
    A reference to a class with the same name is needed to instantiate the class.
  
    **Example 1:**
    ```
    !Object
      var1: value1
      var2: value2
      var3: value3
    ```

    **Example 2:**
    ```
    !Object("apples", 12)
    ```

- Tag - A tag is made by starting with `<tag_name>`, closing with `</tag_name>`,
    and putting content in the middle. Tags that do not need content can be
    done this way: `<tag_name/>`  
    A reference to a function, that will decode the tag is needed. 
    - Tags that start with `<tag_name>` will pass content between the tags as text (string) to the function
    - Tags can be added into a pipeline using vertical bar - "|" between tags, which means that the
      result of the left tag will be passed into right tag.

    **Example 1:**
    ```
    <tag>Content</tag>
    ```
    **Example 2:**
    ```
    <l|tag>Path</l|tag>
    ```
    **Example 3:**
    ```
    <tag/>
    ```
    **Default tags:**  
    `<l>Path</l>` - load and insert content from external file, if file has .yam extention, it will be parsed.  
    `<time/>` - get current UNIX timestamp.


### File structure
In examples, each block is considered a file. Yam files have .yam extension.  
File base (where indent is 0) can contain either a list, a hashtable/dictionary or object, can't be mixed. Indent is 2 spaces.  

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
  3.14159
Fruits:
  Apples:
    Tasty
  Pears:
    Okay
```

Base object:
```
!Display
  menu: <l>pages/index.html</l>
  options: <l>pages/options.html</l>
  log_path: logs/display.log
  settings:
    width: 1920
    height: 1080
    mode: fullscreen
  show_hidden: false
```
