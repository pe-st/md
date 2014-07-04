markdown
========

Personal notes in markdown notatino or about markdown


## Markdown

* The [original][gruber]
* Github Help: [Basics][basics]
* Github Help: [Writing on GitHub][wog]
* Github Guide: [Mastering Markdown][mm]

## Markdown on GitHub

Markdown [dialect][gfm] used with GitHub.

Most notable differences:

### Fenced Code Blocks

Code fenced with three backticks instead of indenting 4 spaces:

    ```
    hello world;
    ```

becomes:

```
hello world;
```

### Syntax highlighting

Like fenced code blocks, but adding a language type after the three backticks:

    ```C++
    int main() {
       cout << hello world;
    }
    ```

becomes

```C++
int main() {
   cout << hello world;
}
```




[gruber]: http://daringfireball.net/projects/markdown/
[basics]: https://help.github.com/articles/markdown-basics
[gfm]:    https://help.github.com/articles/github-flavored-markdown
[mm]:     https://guides.github.com/features/mastering-markdown
[wog]:    https://help.github.com/articles/writing-on-github
