# python

## Stuff I don't like about python

- indentation too important and error prone
  (e.g. changing indentation for refactoring is a 'red' difference in Beyond Compare, not a 'blue' one as in other languages)
- no constants (just UPPER_CASE convention, doesn't stop from changing; and pylint allows constants only in top level scope)


## python 2 vs python 3

https://docs.python.org/3/howto/pyporting.html


## Mac 2018-04-16

- macOS Sierra 10.12.6: Python 2.7.10 (no pip out of the box)
- Homebrew (brew install python@2): Python 2.7.14
- Homebrew: Python 3.6.5
- https://docs.brew.sh/Homebrew-and-Python

## Install Python

with `su - admin`:

- `brew install python@2`

### updates

Recommended by brew

- `pip2 install --upgrade pip setuptools wheel`
- `pip3 install --upgrade pip setuptools wheel`

These might work also

- `sudo -H pip2 install --upgrade pip`
- `sudo -H pip3 install --upgrade pip`


## idiomatic python

https://web.archive.org/web/20171207115720/http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html


## pytest

- `pip2 install -U pytest`

- http://pythontesting.net/framework/pytest/pytest-introduction/

### Running Tests

- `py.test gcexport_test.py`


## pylint

- Python Style Guide https://www.python.org/dev/peps/pep-0008/
- https://www.pylint.org/
- https://pylint.readthedocs.io/en/latest/index.html
- https://pylint.readthedocs.io/en/latest/faq.html
- List of messages https://pylint.readthedocs.io/en/latest/technical_reference/features.html
- Another list of messages (incomplete but better explanations) http://pylint-messages.wikidot.com/all-messages

### pylintrc

- order of names checked: ./pylintrc, ./.pylintrc etc (complete list: https://pylint.readthedocs.io/en/latest/user_guide/run.html)
- create example pylintrc:
  `pylint --disable=line-too-long --generate-rcfile > .pylintrc`

### pylint python2 vs python3

https://stackoverflow.com/a/22318936/3686 : Pylint is using the builtin Python parser, and also get standard library information on demand, so the Python version running Pylint has a high impact on its output.

Workaround (when pylint is installed for python 2.7):

- pylint gcexport.py > lint2.txt
- python3 /usr/local/bin/pylint gcexport.py > lint3.txt

