regex stuff
===========

## sites dedicated to regexes

[reg-exp.info]: http://www.regular-expressions.info

- [regular-expressions.info][reg-exp.info]


## regex examples

### AND condition

Using 'non-consuming' regex: `(?=expr)`

e.g. lines that contain HB and MC|MK : `(?=.*HB)(?=.*(MC|MK))`

See also http://stackoverflow.com/questions/469913/regular-expressions-is-there-an-and-operator
