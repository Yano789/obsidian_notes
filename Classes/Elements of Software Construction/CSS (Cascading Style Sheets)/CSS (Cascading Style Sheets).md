a language used in describing the presentation of a document

**Syntax:** *selector {declaration;}* 
- selector can be a reference to id, class, tag, attribute, combinations, and children/siblings of elements
- declarations is written in *property:value* format

example:
![[CSS-1.webp]]
## Selectors
Selects [[HTML (Hyper Text Markup Language)]] elements you want to style
1. **element** - HTML elements based on element name
2. **id** - HTML elements based on id attribute **(#id)** 
3. **class** - HTML elements with class=*class name* will be chosen **(.class)**
4. **universal** - all HTML elements

##  Combinators
Something that explains the relationship between *selectors*
1. **descendant** - matches all elements that are descendants of the elements **(div element)**
2. **child** - all elements that are the children of the element **(div > element)**
3. **sibling** - select an element directly after another element **(div + element)**
4. **subsequent-sibling** - selects all elements that are next siblings of a specified element **(div ~ element)**