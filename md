#!/bin/bash
DIRNAME=`dirname "$1"`
BASENAME=`basename "$1"`

# TMP must be absolute!
TMP=/tmp/md_view_tmp.html

function generate_html {
    rm -f $TMP
    echo '<!DOCTYPE html>' > $TMP
    echo '<html lang="en"' >> $TMP
    echo '<head>' >> $TMP
    echo '<meta charset="utf-8">' >> $TMP
    echo '<meta name="viewport" content="width=device-width, initial-scale=1">' >> $TMP
    echo "<title>$1 - Markdown Preview Window</title>" >> $TMP
    echo '<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/2.10.0/github-markdown.min.css">' >> $TMP
    echo '<style>' >> $TMP
    echo '.markdown-body {box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px;}' >> $TMP
    echo '@media (max-width: 767px) {.markdown-body {padding: 15px;}}' >> $TMP
    echo '</style>' >> $TMP
    echo '<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML">' >> $TMP
    echo '</script>' >> $TMP
    echo '</head>' >> $TMP
    echo '<body class="markdown-body">' >> $TMP
    cd "$DIRNAME"
    Markdown.pl --html4tags "$BASENAME" >> $TMP
    cd - >> /dev/null
    echo '</body>' >> $TMP
    echo '</html>' >> $TMP
}

function usage {
    echo -e "MD - The Markdown Viewer 0.3 - Copyright (c) 2012-2018 Szymon Wrozynski"
    echo -e "Licensed under the MIT License. More details here: https://github.com/szw/md"
    echo -e "Usage: $0 [file_name [target_name]]"
}

if [ -z "$1" ]; then
    usage
else
    generate_html
    if [ -z "$2" ]; then
        if [ $(uname -s) = "Darwin" ]; then
            open $TMP
        else
            xdg-open $TMP
        fi
    else
        mv $TMP $2
    fi
fi
