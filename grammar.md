# Grammar
```
root        ->  ( dictionary | list )

dictionary  ->  <DICT_KEY> (  
                value | object | inline-list  
                | <INDENT> ( value | object | inline-list | dictionary | list )  
                )

list        ->  ( <LIST_ENTRY> ( value | dictionary | object | inline-list ) )*  
                | <LIST_INNER> ( value | dictionary | object | inline-list ) ( <INDENT> list )*

inline-list ->  value (<BAR> value)*

value       ->  ( <NUMBER> | <TEXT> | <BOOL> | <MULTILINE> | <TAG> )

object      ->  <OBJECT> ( <INDENT> dictionary )*
```

# Tokens
```
NUMBER
TEXT
MULTILINE
BOOL
DICT_KEY
LIST_ENTRY
LIST_INNER
OBJECT
TAG
INDENT
BAR
```
