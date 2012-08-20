#!/bin/bash

export TMP=/tmp/md_view_tmp.html

function run_md {
    rm -f $TMP
    echo '<!DOCTYPE html>' > $TMP
    echo '<html lang="en"' >> $TMP
    echo '<head>' >> $TMP
    echo '<meta charset="utf-8" />' >> $TMP
    echo "<title>$1 - Markdown Preview Window</title>" >> $TMP
    echo '<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>' >> $TMP
    echo '</head>' >> $TMP
    echo '<body>' >> $TMP
    Markdown.pl --html4tags $1 >> $TMP
    echo '</body>' >> $TMP
    echo '</html>' >> $TMP
    xdg-open $TMP
}

function usage {
    echo -e "MD - The Markdown presentation tool - Copyright (c) 2012 Szymon Wrozynski"
    echo -e "Licensed under the MIT License. More details here: https://github.com/szw/md"
    echo -e "Usage: $0 [file_name]"
}

if [ -z "$1" ]; then
    usage
else
    run_md $1
fi
