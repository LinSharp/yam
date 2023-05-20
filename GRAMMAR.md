# Grammar
```
root        ->  ( dictionary | list )

dictionary  ->  <DICT_KEY> (  
                value | object | inline-list  
                | <INDENT> ( value | object | inline-list | dictionary | list )  
                )

list        ->  (
                <LIST_ENTRY> ( value | dictionary | object | inline-list )  
                | <LIST_INNER> ( value | dictionary | object | inline-list ) ( <INDENT> list )*
                )*

inline-list ->  value (<BAR> value)*

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

OBJECT      ->  '!Object_name'

TAG         ->  <|tag_name|> | <tag_name>Content</tag_name>

INDENT      ->  '  '

BAR         ->  '|'
```
