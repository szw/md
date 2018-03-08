# MD

The [Markdown](https://daringfireball.net/projects/markdown/) Viewer - version 0.3


## Instalation

Use curl or wget to download [Markdown.pl](http://daringfireball.net/projects/downloads/Markdown_1.0.1.zip) script. Then set it as an executable
and copy it somewhere on your *$PATH*.

    $ curl -O http://daringfireball.net/projects/downloads/Markdown_1.0.1.zip
    $ unzip Markdown_1.0.1.zip
    $ cd Markdown_1.0.1
    $ chmod +x Markdown.pl
    $ sudo cp Markdown.pl /usr/local/bin

Finally, get **md** script, set is as an executable file and copy it like above:

    $ curl -O https://raw.github.com/szw/md/master/md
    $ chmod +x md
    $ sudo mv md /usr/local/bin


## Usage

    md your_markdown_file.md

or (if you want just the generated HTML):

    md your_markdown_file.md your_target_file.html

In the second case, the generated file will not be opened in the browser.

Examples:

    $ md README.md
    $ md my_text.markdown
    ...

In Vim you might use:

    :!md filename

### Mathematics

The viewer can also render math formulas using [MathJax](https://www.mathjax.org). For more information about the Math rendering check [this MathJax quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## Vim snippet

You can easily integrate **md** with Vim. The following snippet set **md** as
a Vim command, accessed via `:Md`:

    au FileType markdown command! -buffer -nargs=0 Md :silent! :exe '! md "' . expand('%:p') . '"' | redraw!


## Sublime Text 3 Build System

You can easily plugin the viewer into ST3 Build System. Create a file in your `Packages/User` directory (on macOS it could be `~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User`) named `Markdown\ Preview.sublime-build` the following content:

    {
        "selector": "text.html.markdown",
        "working_dir": "$project_path",
        "path": "~/.local/bin",
        "shell_cmd": "md $file"
    }

<small>_`path` is necessary only if you put `md` in a non-standard place (like here `~/.local/bin`)._</small>

Afterwards, you can easily render Markdown by pressing (in case of macOS) <code>&#8984;</code> + `B`.

If you have more Markdown related build systems already, you can change the default one using <code>&#8679;</code> + <code>&#8984;</code> + `B`.


## License & copyright

Copyright &copy; 2012-2018 Szymon Wrozynski and Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
