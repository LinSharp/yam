# Grammar

## Leader
```
|  - seperates optons
() - a group of options
*  - previos statement is multiplied 0 or more times
*1  - previos statement is multiplied 1 or more times
-> - explains how to make the nonterminal
```

## Dictionary
```
root        ->  dictionary | list

dictionary  ->  <DICT_KEY> (  
                value | inline-list  
                | <NEWLINE>(<INDENT>)*1 ( value | object | inline-list | dictionary | list )  
                )

list        ->  (
                <LIST_ENTRY> ( value | dictionary | object | inline-list )  
                | <LIST_INNER> ( value | dictionary | object | inline-list ) ( <INDENT> list )*
                )*

inline-list ->  value (<BAR> value)*1

value       ->  ( <NUMBER> | <TEXT> | <BOOL> | <MULTILINE> | <TAG> )

object      ->  <OBJECT> ( <INDENT> dictionary )*
```

# Tokens
```
NUMBER      ->  124 | 3.14 | 32% | 14/32

TEXT        ->  apple | "3.14 oranges"

MULTILINE   ->  """
                Multi
                line
                text.
                """

BOOL        ->  true | false

DICT_KEY    ->  key_name:

LIST_ENTRY  ->  '- '

LIST_INNER  ->  '---'

OBJECT      ->  !Object_name

TAG         ->  <|tag_name|> | <tag_name>Content</tag_name>

INDENT      ->  '  '

BAR         ->  '|'

NEWLINE     ->  '\n'
```
