ruby notes
==========

## documentation

- http://www.ruby-doc.org/

- Pragmatic Programmer's Guide ("Pickaxe Book"): http://ruby-doc.com/docs/ProgrammingRuby/
- Ruby Programming: http://en.wikibooks.org/wiki/Ruby_Programming
- Seven Languages in Seven Weeks (7li7w)
  - see also http://github.com/pe-st/7li7w/ruby


## interpreter

`irb`

- find out ruby's version in irb: `RUBY_VERSION`


## conventions

From 7li7w:
- Classes start with capital letters and typically use CamelCase to denote capitalization.
- You must prepend
  - instance variables (one value per object) with @ and
  - class variables (one value per class) with @@.
- Instance variables and method names begin with lowercase letters in the underscore_style.
- Constants are in ALL_CAPS.
- Functions and methods that test typically use a question mark (if test?).


## Classes

- method `initialize` has special meaning. Ruby will call it when the class instantiates a new object.
- instance variables:
  - `attr`, defining an instance variable and a method of the same name to access it
  - `attr_accessor`, defining an instance variable, an accessor, and a setter.


## Blocks

- { ... }
- do ... end

Convention: braces for blocks on one line, do/end for multiple lines
