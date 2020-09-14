# XPath cheat sheet

## Google chrome

- Open Dev console (F12)
- Press Ctrl+F on elements panel
- Type XPath in search bar to match elements

## Evaluate

- In dev console use `$x('XPATH'[, $0])` (where `$0` is the selected element or current node)


## XPath expressions and meanings

- `./*` - all nodes under the current node
- `.//*` - all nodes including all descendant nodes
- `/*` - select root node (`html`) regardless of current node
- `//*` - select all nodes in document regardless of current node
- `//*[@id="id" or @type="submit"]` - find element which has id="id" or type="submit"
 
- `//*[@class and @ping]` - select all elements which contain attributes `class` and `ping`
- `//*[not(@class)]` - select all elements do not have a class attribute

- `./../.` - select parent node of current element (same as `../.`)
- `..//h3[1]` - find first `h3` tag in parent element (*note* Arrays starts at `1` not `0`)

- `./text()` - select all the text only nodes under current node (but won't select any html tags or text inside html tags)

- `. | .//h3 | ../../*[2]` - link, title, description of a google search result (where `a` is the current node)

- `//*[@*="s"]` - Any element in the document which has *any* attribute with value = 's'

## XPath Axes

Always used like `axis::selector`. Most of the time it is better to use `.` or `//` instead of `self`, 
`descendant`, etc. But the following are useful

- `ancestor` - `./ancestor::*` - get all parents of current node until root
- `ancestor-or-self` - similar to jQuery closest, i.e. `.//ancestor-or-self::div` to find closest div
- `following` - `./following::div` - get all divs after current node (doesn't matter if child, as long as it is a div that comes after current element it matches)
- `following-sibling` - `./following-sibling::div` - more useful. Only gives sibling elements that come after current node.
- `preceding` / `preceding-sibling` - same as above but preceding
- `descendant-or-self` - same as `. | .//*`
- `self` - useful to refer to current node, .e.g `self::node()`

## Useful Functions
- `not()` - invert the selection
    - Examples:
        - `'//h3[not(@class="s")]'` - Select all h3 node which don't have `s` class   

- `contains()` - checks for partial text match
    - Examples:
        - `'.//*[contains(., "get")]'` - Select any node that contains the word `get`   

- `starts-with` and `ends-with` - similar to contains

- `text()` - returns text node (best for exact match)
    - Examples:
        - `'.//*[text() = 'get']'` - Select any node that has the exact word `get`   

- `node()` - return node value.

- `comment()` - returns comment node.

- `position()` - return the position of an element in the list.
    - Examples:
        - `'.//h3[position()=1]'` - Select h3 node at position 1 in list 

- `name(node_expression)` or `local-name` - return the string name of the last expression.
    - Examples:
        - `'./*[name()="h1" or name()="h2" or name()="h3"]'` - All type of headings 

- `count(node_expression)` - count number of element in a specified node.
    - Examples:
        - `count(*)` - Return number of children 
        - `.//div[count(.//span) = 1]` - Select all divs with only one span element
        - `//ul[count(li) > 2]` - select all lists with more than 2 items

- `last` or `first`
    - Examples:
        - `//a[first]` - first a tag    
        
## Predicates

- Like array index but starts at `1` instead of 0
- Does not necessarily have to contain numbers

- Examples:
    - `//a[1]` - first a test
    - `'//div[.//a[@ping]]'` - find divs that have `a` tag with attribute `ping`
        