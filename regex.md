regex stuff
===========

## sites dedicated to regexes

[reg-exp.info]: http://www.regular-expressions.info

- [regular-expressions.info][reg-exp.info]


## regex examples

### AND condition

Using 'non-consuming' regex: `(?=expr)`

e.g. lines that contain HB and MC|MK : `(?=.*HB.*)(?=.*(MC|MK).*)`

