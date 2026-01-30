# Key-value formats

## Configuration files
Software sometimes need to be cofigured
- command line arguments
- environment variables
- configureation files
  - RDF turtle (Apache Jena Fuseki)
  - XML (Apache Solr)
  - JSON (Drupal)

## .properties
Used for holding configuration
- Java specific
  - ISO-8859-1 (Latin 1)
- is a hash table
- also used for localizations/translations
- has XML version

```
# Port used by storage REST API.
storage.port = 8083

# Windows ex: C:\\Users\\Kuba\\Documents\\GitHub\\etl\\deploy\\jars
# Linux ex: /opt/lp/etl/deploy/jars
storage.jars.directory = ./jars

# Directory used by the storage.
# Windows ex: C:\\Tools\\lp\\etl\\storage
# Linux ex: /data/lp/etl/storage
storage.directory = ./data
```

## INI
Used for holding configuration
- originally from MS-DOS
  - replaced by Windows Registry
  - but present even in Windows 11
- human readable, simple to parse
- not really standardized
- no nesting

dbsettings.ini
```
; last modified 1 April 2001 by John Doe
[owner]
name=John Doe
organization=Acme Widgets Inc.

[database]
; use IP address in case network name resolution is not working
server=192.0.2.62     
port=143
file="payroll.dat"

```

## TOML (Toms Obvious, Minimal Langauge)
2021
"a config format for humans"
- human readable, writable
- easily parsed
- maps to a hash table
- native data types
- unicode
File extension: .toml
Media type: application/toml

```
#This is a TOML document

title = "TOML Example"

[owner]
name = "Tom Preston-Werner"
dob = 1979-05-27T07:32:00-08:00

[database]
enabled = true
ports = [ 8000, 8001, 8002 ]
data = [ ["delta", "phi"], [3.14] ]
temp_targets = { cpu = 79.5, case = 72.0 }
```
### Comments
```
# This is a TOML document
```

### Keys and key-value pairs
3 types of keys
```
bare-key = "value"
"quoted key" = "value"
dotted.key = "value"
```

### Strings
4 types
1. basic string - no line breaks, no newlines, supports \ escaping
```
basic_string = "TOML Example"
with_escapes = "You can \"quote\" me."

You can "quote" me
```
2. multiline string - basic string with newlines and escaping
```
multiline = """\
  The quick brown \
  fox jumps over \
  the lazy dog.\
```
3. literal string - no escaping applied
```
literal = '\\User\admin$\system32'
```
4. multiline literal - first newline after ’’’ trimmed, all other preserved
```
multi_line_literal = '''
The first newline is
trimmed in raw strings.
   All other whitespace
   is preserved.
```

### Numbers
- int
- hexadecimal (0x)
- octal (0o)
- binary (0b)
- float
- infinity
- not a number


### Date and times
offset (with timezone)
```
# offset datetime
odt1 = 1979-05-27T07:32:00Z
odt2 = 1979-05-27T00:32:00-07:00
```
local (without timezone)
```
# local date
ld1 = 1979-05-27
# local datetime
ldt1 = 1979-05-27T07:32:00
# local time
lt1 = 07:32:00
```
### Boleans
- true
- false

### Arrays
trailing comma - important for automated generation - no need to check whether an item is the last one

'''
integers = [ 1, 2, 3 ]
colors = [ "red", "yellow", "green" ]
nested_arrays_of_ints = [ [ 1, 2 ], [3, 4, 5] ]
nested_mixed_array = [ [ 1, 2 ], ["a", "b", "c"] ]
string_array = [ "all", 'strings', """are the same""", '''type''' ]

integers3 = [
  1,
  2, # this is ok
]
'''

### (Hash)tables
Collection of key-value pairs
(same as section in INI)
```
[table-1]
key1 = "some string"
key2 = 123

[table-2]
key1 = "another string"
key2 = 456

#inline table
name = { first = "Tom", last = "Preston-Werner" }
point = { x = 1, y = 2 }
animal = { name = "pug" }

#inline table
name = { first = "Tom", last = "Preston-Werner" }
point = { x = 1, y = 2 }
animal = { name = "pug" }
```

### Nested tables
```
physical.color = "orange"
physical.shape = "round"

#same as:
[physical]
color = "orange"
shape = "round"

[servers.alpha]
ip = "10.0.0.1"
role = "frontend"

[servers.beta]
ip = "10.0.0.2"
role = "backend"

#structure in JSON:
{
    "servers": {
        "alpha": {
            "ip": "10.0.0.1",
            "role": "frontend"
        },
        "beta": {
            "ip": "10.0.0.2",
            "role": "frontend"
        }
    }
}


```

### Array of tables
```
[[products]]
name = "Hammer"
sku = 738594937

[[products]]  # empty table within the array

[[products]]
name = "Nail"
sku = 284758393

```
```
points = [ { x = 1, y = 2, z = 3 },
           { x = 7, y = 8, z = 9 },
           { x = 2, y = 4, z = 8 } ]

# same as:
[[points]]
x = 1
y = 2
z = 3

[[points]]
x = 7
y = 8
z = 9

[[points]]
x = 2
y = 4
z = 8
```

### Libraries

### Usage
Traefik
- cloud-based HTTP proxy
- alternatively YAML

Poetry
- python dependency and packaging management

GitLab runner
- app that works with GitLab CI/CD to run jobs in a pipeline



## YAML (YAML Aint Markup Language)
"YAML is a human friendly data serialization standard for all programming"

Primary for configuration, but an be used for generic data serialization as well
- unicode
- human readable
- machine parseable

File extension: .yaml, .yml
Media type: application/yaml

[YAMLint ](http://www.yamllint.com/)(YAML Validator)

```
---
# An employee record
name: Martin D'vloper
job: Developer
skill: Elite
employed: True
foods:
  - Apple
  - Orange
  - Strawberry
  - Mango
languages:
  perl: Elite
  python: Elite
  pascal: Lame
education: |
  4 GCSEs
  3 A-Levels
  BSc in the Internet of Things
```

### Sequence/Array/List
dash, space, value
```
- name
```
values = called scalars

Alternative array syntax, compatible with JSON arrays

```
# A list of tasty fruits
- Apple
- Orange
- Strawberry
- Mango

['Apple', 'Orange', 'Strawberry', 'Mango']
```

### Document boundaries
One YAML file may contain multiple documents, they are separated by "---". Usefull for streaming

```
# A list of tasty fruits
---
- Apple
- Orange
- Strawberry
- Mango
...
---
- Papaya
- Clementine
- Peach
- Pineapple
---
```

### Mapping/map/dictionary/hash
Indentation is part of YAML syntax

format:
```
key: value
```
Example:
```
# An employee record
name: Martin D'vloper
job: Developer
skill: Elite
```
inline map alternative syntax, compatible with JSON Object

JSON file is a valid YAML 1.2 file

```
martin: {name: "Martin D'vloper", job: "Developer", skill: "Elite"}
```

### Multiline strings
Indentation is ignored in both cases

```
fold_newlines: >
            this is really a
            single line of text
            despite appearances
```

```
include_newlines: |
            exactly as you see
            will appear these three
            lines of poetry
```

### Common errors
- colon in value -> must be queted
- in double quetes can escapes be used 

### YAML libraries


### Usage
- ansible playbooks
- Docker compose
- Kubernetes
- RESTful web services docs - swagger


## Alternatives
- HOCON
- JSON5
- StrictYAML: type-safe YAML parser