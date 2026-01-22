# XQuery
- complex queries and trasformations
- contains XPath
Versions: 1.0 (2007), 3.0 (2014),  3.1 (2017)
- keyword must always be in lowercase
- functional query language


## Expressions
- Path expressions (XPath)
- FLWOR expressions (for, let, where, order by, return)
- Conditional expressions (if, then, else)
- Quantified expressions (some/every, satisfies)
- Boolean expressions (and, or, not)
- Primary expressions (literal, variable references, function calls, constuctors)


## Node constructors
Allows for creation of new nodes for elements, attributes

### Direct constructor
Well-formed XML fragment with embedded query expressions
- names of elements and attributes must be fixed
 
```
<movies>{ count(//movie) }</movies>
```
- attribute
- Element content

Embedded query expressions - enclosed by "{}"

```
//Create a summary of all movies
<movies>
    <count>{ count(//movie) }</count>
    {
        for $m in //movie
        return
            <movie year="{ data($m/@year) }">{ $m/title/text() }</movie>
    }
</movies>

```

### Computed constructor
Special syntax
- names of elements and attributes can be dynamic

1. Element node
2. Attribute node
3. Text node

```
element movies { count(//movie) }
```

```
/// Create a summary of all movies
element movies {
    element count { count(//movie) },
    for $m in //movie
    return
        element movie {
            attribute year { data($m/@year) },
            text { $m/title/text() }
        }
}
```


### FLWOR expressions
- allow for advanced iterations over sequence of items

Clauses:
- for
- let
- where
- order by
- return

```
for $m in //movie
let $r := $m/@rating
where $r >= 75
order by $m/@year
return $m/title/text()
```

usecases:
- querying
- joining
- grouping
- aggregation
- integration
- transformation
- validation

#### For 
Iterates over items of one or more input sequences - which are accessible via the introduced variables
- optional positional variable - allows to access the ordinal number of the current item
- 

#### Let 
Defines one or more auxiliary variable assignments

#### Where
Allows to describe comples filtering conditions
- items not satysfying the condition are skipped

#### Order by
Defines the order of proccess
- ascending
- descending

#### Return 
Defines how the result sequence is constructed

### Conditional expressions

- else branch is compulsory
    - if needed empry sequence () can be returned if needed

```
if (count(//movie) > 0)
then <movies>{ string-join(//movie/title, ", ") }</movies>
else ()
```

### Switch expression
- the first matching branch is chosen and its return clause is evaluated and the result returned
- defaulte branch is compulsory, must be provided as the last option

```
for $m in //movie
return
<movie>
	{ $m/title }
	{
	switch (count($m/actor))
	case 0 return <no-actors/>
	case 1 return <actor>{ $m/actor/text() }</actor>
	default return <actors>{ string-join($m/actor, ", ") }</actors>
	}
</movie>
```

### Quantified expression
Quantifier returns true if and only if 
- some (at least one item)
- every (all the items)
of given sequence/s satisfy the provided condition

```
for $a in distinct-values(//actor)
where
    every $m in //movie satisfies $m/actor[text() = $a]
return $a
```

```
//Find titles of movies in which Ivan Trojan played
for $m in //movie
where
    some $a in $m/actor satisfies $a = "Ivan Trojan"
return $m/title/text()
```


### Extended FLWOR Expressions
(XQuery 3.0)

- window - sliding or tumbling windows to iterate over
- group by - equality-based groupings of input items
- count - positional numbers of tuples in a stream

#### For 
- optional "allowing empty"
() is considered instead of an empty sequence
- positional variable = allows to access the ordinal number of the current item

#### Group by
Performs equality-based grouping defined by one or more grouping variables

#### Window clause 
- allows to iterate over the generated windows
    1. tubling mode
    2. sliding mode
window = sequnece of consecutive items from the input
- accessible via the main variable
- contains the start item, end item, and all items between them

##### Start condition
start item = item that satisfies a given condition

##### End condition
end item = first item that satisfies a given condition
if such an item cannot be found
- the last item is the very last input item
- only in case the "only" keyword is not specified
- otherwise such a window is not generated at all

##### Window variables (optional)
Bound to the first/last item
- at = bound to the ordinal position of the first/last item
- previous = bound to the item that precedes the first/last item
- next = bound to the item that follows the first/last item


##### Tumbling window
Search for the start item of the next windows begins with the item that follows the end item of the previous window
-> windows never overlap (input item may never be found in multiple windows)
if the end condition is missing 
    - all start items are first detected 
    - each window terminated by the item that precedes the next  

##### Sliding window
Every item that satisfies the start condition become the starting item of a new window
-> windows may overlap (input item may be found in multiple windows)


### Count clause
Allows to access the ordinal number of the current tuple in a stream

count $var_name