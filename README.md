# yaml-files
An overview of how YAML files is structured and some exemples how to use them


YAML is often used for configuration files and data exchange between systems

YAML uses indentation and whitespace to define its structure, which makes it highly readable and easy to understand, but also easy to have a typo, commum issue when you use it as config template such as for Kubernetes or Docker administration.

YAML supports several data types, including scalars (strings, numbers, booleans), sequences (arrays or lists), and mappings (key-value pairs or dictionaries). These data types can be nested within each other creating a complex data structures.

As other languages YAML allows adding comments to the file using the "#" symbol.

Key-Value Pairs:
    name: John Doe
    age: 30

Sequences:

fruits:
  - apple
  - banana
  - orange

YAML supports nesting data structures. This means you can have key-value pairs inside key-value pairs, or sequences inside sequences, creating hierarchical structures. The indentation is crucial for maintaining the structure and readability.

person:
  name: John Doe
  age: 30
  address:
    street: 123 Main St
    city: Anytown
    country: USA

YAML provides the ability to create anchors and aliases to reference the same data at multiple points within the file. This feature helps avoid redundancy and allows for efficient reuse of data. An anchor is defined using the ampersand (&) symbol, and an alias is denoted by the asterisk (*) symbol.

Anchors and Aliases

# Define an anchor for a complex mapping
person: &person_anchor
  name: John Doe
  age: 30
  address:
    street: 123 Main St
    city: Anytown
    country: USA

# Create an alias to reference the anchor
friend: *person_anchor

YAML offers different scalar styles for strings, including plain, single-quoted, and double-quoted. Each style has its own rules regarding escaping special characters and whitespace, I know!! It can be a mess.

# Plain Style

name: John Doe
age: 30

# Single-Quoted Style

message: 'Hello, World!'

#Double-Quoted Style

greeting: "Hello, $name!"

# Folded Style

description: >
  This is a long
  multiline description
  that will be folded
  into a single string.

# Literal Style

content: |
  This is a literal
  multiline string
  that will be preserved
  exactly as written.

  YAML supports including content from external files using the << or !include directive. This feature allows you to split YAML files into smaller, reusable components.

# Inclusion ussing '<<'

# config.yml
defaults: &defaults
  timeout: 5000
  max_retries: 3

api_settings:
  <<: *defaults
  endpoint: https://api.example.com

# database.yml
<<: include config.yml

db_settings:
  <<: *defaults
  host: localhost
  port: 3306

# Using the !include Directive

# main.yml
name: John Doe
age: 30
address: !include address.yml

# address.yml
street: 123 Main St
city: Anytown
country: USA
