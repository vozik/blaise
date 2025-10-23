---



\## \*\*1. PSI-L Syntax Rules\*\*



1\. \*\*Optional modifier appears at the end\*\*, separated by a comma:



&nbsp;  \* `@string, optional`

&nbsp;  \* `list of @argument separated by ',', optional`

&nbsp;  \* `single from @color, optional`

&nbsp;  \* `multiple from @color, optional`



2\. \*\*List separator rule remains the same\*\* (`separated by 'CHAR'`).



3\. \*\*Enumerated selections\*\* follow the same optional placement:



&nbsp;  \* `single from @enum, optional`

&nbsp;  \* `multiple from @enum, optional`



4\. \*\*Type references\*\* remain unchanged:



&nbsp;  \* `@string`, `@number`, `@boolean`, `@argument`



---



\## \*\*2. Examples\*\*



```text

@string, optional

@number

@boolean

list of @argument separated by ',', optional

list of @argument separated by ','

single from @color, optional

multiple from @color, optional

single from @color

multiple from @color

```



---



\## \*\*3. Updated Quick Reference Table (Optional at End)\*\*



| \*\*Element\*\*                  | \*\*Syntax / Example\*\*                           | \*\*Description\*\*                                                   |

| ---------------------------- | ---------------------------------------------- | ----------------------------------------------------------------- |

| \*\*Type Reference\*\*           | `@string`, `@number`, `@boolean`, `@argument`  | Refers to a built-in or user-defined type.                        |

| \*\*Optional Field\*\*           | `@string, optional`                            | Field may be omitted. Optional appears at the end, after a comma. |

| \*\*List of Values\*\*           | `list of @argument separated by ','`           | Multiple values of the same type.                                 |

| \*\*Optional List\*\*            | `list of @argument separated by ',', optional` | List may be omitted.                                              |

| \*\*Enum — Single\*\*            | `single from @color`                           | Exactly one value chosen from a predefined set.                   |

| \*\*Enum — Single Optional\*\*   | `single from @color, optional`                 | Single value from enum, may be omitted.                           |

| \*\*Enum — Multiple\*\*          | `multiple from @color`                         | One or more values from a predefined set.                         |

| \*\*Enum — Multiple Optional\*\* | `multiple from @color, optional`               | Multiple values from enum, may be omitted.                        |



---



\### ✅ \*\*Notes\*\*



\* This keeps \*\*optional modifier consistent\*\* across all types, lists, and enum selections.

\* The language remains \*\*flat, readable, and fully parseable\*\*.

\* No ambiguity: optionality is \*\*always at the end\*\* after a comma.



