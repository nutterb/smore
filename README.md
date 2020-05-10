# Smore

(I'm not attached to the name. It was the first thing that popped into my head)

## Structure of a Table

Tabular data consists of four core elements, each of which may be treated separately.  These elements are:

1. Header
2. Body
3. Intermediate Footer (a footer that may be placed inbetween sections of a table, such as in LaTeX::longtable)
4. Table Footer (the footer placed at the very end of the table after all sections have been printed)

## Principles of Table Metadata management

1. The original source data for the table is stored as an attribute of the object.
2. Attributes may be altered for any single cell of a table.
3. Attributes for a cell are stored in Entity-Attribute-Value format in order to minimize memorize size of the meta data object. (Entity in this context may mean row, column, and table part)
4. Any manipulations to the data are stored as expressions and are not applied to the data until immediately before rendering the table.
5. Object retains meta data for general table attributes in addition to cell-specific attributes.


## Implementation Thoughts

* object needs the following attributes
  + data
  + cell attributes
  + table attributes
* Package comes with zero/minimal dependencies (Ideally, the only dependency would be something like `assertthat` or `checkmate`
* Uses very little non-standard evaluation (if any). (may not be entirely possible if any manipulation of the data is to be allowed. Ideally, I would think capturing expressions would be sufficient)


### Basic cell-attributes to support

* italic
* bold
* horizontal-align (left, center, right)
* vertical-align (top, middle, bottom)
* background-color
* text-color
* text-font
* cell-height
* cell-width
* round

### Others to consider support

We could either define these, or leave them for extension packages to define

* border-bottom
* border-top
* border-left
* border-right
* pad-left
* pad-right
* pad-top
* pad-bottom
* rotation
* missing-string (na-string)
* replacement (simply replace the contents of a cell)
* expression
* sanitize

## Basic table-attributes to support

* table-number
* caption
* label
* horizontal-align
* longtable

### Others to consider supporting

We could either define these, or leave them for extension packages to define

* hhline
* bookdown
* float
* booktabs


## Extending

While the package may have some basic utilities for producing tables, extension packages would be able to define additional attributes and the functions to apply those to cell values and format the tables appropriately. I'm thinking the easiest thing to do would be to have each attribute have an identically named function at modifies the value.  Then, to extend it, you would only need to write a function to tell the package how to handle the attribute.  But that has a number of pitfalls if you want a function with multiple arguments. Ideas on how to extend the structure are welcome (as well as any ideas on what the generic structure might look like)
