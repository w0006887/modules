# modules

This is a `GitHub` repository that hosts Prof. Tak's instructional content. The majority of the content is located at [his site](http://dtkb.org/~auyeunt/teaches/modules). However, some newer content is being developed here. Some older content is being converted into GitHub Markdown format.

The [directory](directory.md) is automatically regenerated whenever there is an update to the module files. For the [GitHub workflow to work](https://docs.github.com/en/actions/using-workflows), the heading of a module should follow this template:

```markdown
# _Module 1234: title_
```

Also, for the GitHub workflow to work, [the GitHub bot should have read/write permissions](https://github.com/marketplace/actions/github-push).

# Fork, contribute and pull request

If you see an issue, you can fork the file(s), make your edits, and then submit a pull request to merge your contribution to the main branch.

# Tricks, Tips and Caveats

## Set element delimiters

`{` and `}` in an equation are normally specified as `\{` and `\}` in an equation environment. However, the GitHub equation rendering mechanism requires two backslashes.

```markdown
$\{a,b,c\}$ is a set
```

is rendered as "$\{a,b,c\}$ is a set".

However,

```markdown
$\\{a,b,c\\}$ is a set
```

is rendered as "$\\{a,b,c\\}$ is a set".

Using the built-in editor of `github.com`, the following find-and-replace configuration will change `\{` and `\}` to `\\{` and `\\}`:

* Search for `(?:[^\\])(\\[\{\}])`
* Replace with `\\$1`

Note that equation blocks that are standalone (using `$$` to start and end the equation) do not need to escape the backslash. 

```markdown
$$\{a,b,c\}$$

is a set
```
is rendered as follows:

---

$$\{a,b,c\}$$

is a set

---

## No Markdown in HTML elements by default

Markdown content that is nested in HTML content is not rendered. 

```html
<div>
Isn't this **bold**?
</div>
```

is rendered as

<p>
Isn't this **bold**?
</p>

This limitation can be overcome by specifying the nested text is in Markdown.

```html
<p markdown="1">
Isn't this **bold**?
</p>
```

is rendered as follows:

<p markdown="1">
Isn't this **bold**?
</p>


## Set delimiters inside HTML elements

`{` and `}` are rendered correctly with a single backslash in equations inside HTML elements.

```HTML
<div>
$\{a,b,c\}$
</div>
```

is rendered as 

<div>
$\{a,b,c\}$
</div>
