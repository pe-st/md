regex stuff
===========

## Quick Reference

- `??` : lazy variant of greedy `?` (and `?+` is possessive)
- `*?` : lazy variant of greedy `*` (and `*+` is possessive)
- `+?` : lazy variant of greedy `+` (and `++` is possessive)
- `{n,m}? {n,}? {,m}?` : lazy variants of greedy `{n,m} {n,} {,m}` (`{n}` is neither greedy nor lazy, `{n,m}+ {n,}+` are possessive)

- `^` : start of string or line
- `S` : end of string or line

- `\d` and `\D` : digit and non-digit
- `\w` and `\W` : word character and non-word character
- `\s` and `\S` : whitespace and non-whitespace
- `\b` and `\B` : word boundary and non-boundary

- `[]` : character class, literals inside everything except `^-]\` (these must be escaped by `\`)
- `(regex)`, `(?:regex)` and `(?<name>regex)` : capturing group, non-capturing group and named capturing group
- `(?>regex)` : atomic group (no backtracking, like possessive quantifier)

- `(?i)`, `(?-i)` : ignore upper/lowercase modifier and case-sensitive matching resp.
- `(?s)` : single line mode. In single line mode the whole string is one line, i.e. `.` (and `\s`) matches also line breaks
- `(?m)` : multi line mode. `^` and `$` match start and end of every line

- `.` and `\N` : match everything except line break. Only the dot changes behaviour in single line mode, `\N` still doesn't match a line break

### Greedy, Lazy and Possessive

Possessive quantification is similar to greedy, but without backtracking. Example:
`".*"` matches `"abc"` in `"abc"x`, but `".*+"` doesn't.

An atomic group is the same as possessive quantification, just a little longer to write.
Some flavours support atomic groups, but not possessive quantifiers

See https://www.regular-expressions.info/atomic.html and https://www.regular-expressions.info/possessive.html


## sites dedicated to regexes

[reg-exp.info]: https://www.regular-expressions.info
[regexr]: https://regexr.com
[crossword]: https://regexcrossword.com/

- [regular-expressions.info][reg-exp.info]
- [RegExr][regexr]
- [Regex Crossword][crossword]


## regex flavours

- Wikipedia [comparison](https://en.wikipedia.org/wiki/Comparison_of_regular_expression_engines)
- Comparison per feature on [regular-expressions.info][reg-exp.info], e.g. the Basic Features page: choose two flavors in the dropdown and compare

Major flavours (list not exhaustive):

- POSIX: supports `[:digit:]` for digits (same as `[0-9]`)
- Perl: supports `\d` for digits
- Emacs: needs backslashes before `(|){}` (not not before `[]`)
- GNU extensions: no multiline support (at least in egrep); e.g. `\<\>` in addition to `\b\B` as word boundaries
- Boost: can use several flavors (perl, egrep, etc)
- Oniguruma
- Java: smaller set than Perl, e.g. no case conversions in replacements (`\l\u\L\U\E`)
- TRegExpr (Delphi Library): no multi-line regexes?

Flavours in applications:

- GNU extensions: egrep, awk?
- Oniguruma: Sublime Text?
- TRegExpr: TotalCommander


## regex examples

### AND condition

Using 'non-consuming' regex: `(?=expr)`

e.g. lines that contain HB and MC|MK : `(?=.*HB)(?=.*(MC|MK))`

See also http://stackoverflow.com/questions/469913/regular-expressions-is-there-an-and-operator

### Using multiline support in recursive grep

- Use `grep -P` (Perl regex mode) together with `-zo` instead of `grep -E` (GNU Extension regex mode)
  (see https://stackoverflow.com/a/7167115/3686)
- `grep -r -P "regex" . --include=pom.xml` is the slightly cumbersome syntax for recursive grep

Example: all POM files referencing `util:junit`

`grep -r -Pzo "(?s)..\N*util</groupId>\s*<artifactId>junit\N*.." . --include=pom.xml`
