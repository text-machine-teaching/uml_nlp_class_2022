# Usage

To add/update this wiki, simply push `Edit on GitHub` button in the top-right corner. You have to be a part of [github.com/text-machine-lab](https://github.com/text-machine-lab) in order to push directly into the master branch and this is a recommended way to do it. The website is automatically updated after a push to the repository, so you don't need to do anything else (just to wait about a minute or so).

We prefer Markdown over reStructuredText text in this wiki ([cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet), [How to use Markdown for writing Docs](https://docs.microsoft.com/en-us/contribute/how-to-write-use-markdown)) as it is simpler to start with and we want to encourage you to help us maintain this wiki up to date.
If you really need to use reST (we do advise against this as it raises the bar for new people), here's a nice [cheatsheet](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst).

However, do not update either of `make.bat`, `index.rst`, `history.rst`, `conf.py` or `Makefile` without knowing how Sphinx works and what you are actually doing.

### Including images

If you want to include an image to a wiki page, use

```markdown
![My image caption](http://url/to/your/image)
```

for external URLs (preferred method).

In the case of your own images, place them to `docs/img` directory and specify a local path in the markdown

```markdown
![My image caption](./img/my-image.png)
```

You can also use HTML (but keep things simple), for example, if you want to control image size

```html
<img src="./img/my-image.png" width="300"/>
```

OR

```html
<figure>
    <img src='./img/my-image.png' width="300"/>
    <figcaption>My image capiton</figcaption>
</figure>
```


### Maitainer info

This wiki is hosted using [readthedocs.org](https://readthedocs.org/), you can ask Vlad for the credentials. A good example of Sphinx usage (and common python practices) can be found [in this project](https://github.com/audreyr/binaryornot).
