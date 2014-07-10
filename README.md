markdown
========

Personal notes in markdown notation or about markdown


## Markdown

* The [original][gruber]
* Github Help: [Basics][basics]
* Github Help: [Writing on GitHub][wog]
* Github Guide: [Mastering Markdown][mm]

## Markdown on GitHub

Markdown dialect [Github Flavored Markdown][gfm].

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


## Markdown tricks

### Comments

Use HTML comments, e.g.

    <!--
    Local Variables:
    coding: utf-8
    End:
    -->

like at the end of this file to let Emacs known about the coding of this file.

But as this is just HTML, the comment will end up in generated HTML.

If you don't want the comment in the output, you can
[use the link label syntax][so]; the shortest version
is to use `[//]: # (comment)`

    [//]: # (this is a)
    [//]: # (comment)


[gruber]: http://daringfireball.net/projects/markdown/
[basics]: https://help.github.com/articles/markdown-basics
[gfm]:    https://help.github.com/articles/github-flavored-markdown
[mm]:     https://guides.github.com/features/mastering-markdown
[wog]:    https://help.github.com/articles/writing-on-github
[so]:     http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax/20885980#20885980


<!--
Local Variables:
coding: utf-8
End:
-->
