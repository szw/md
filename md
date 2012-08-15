#!/bin/bash

export TMP=/tmp/md_view_

function run_md {
    rm -f $TMP**
    echo '<!DOCTYPE html>' > $TMP$1.html
    echo '<html lang="en"' >> $TMP$1.html
    echo '<head>' >> $TMP$1.html
    echo '<meta charset="utf-8" />' >> $TMP$1.html
    echo "<title>$1 - Markdown Preview Window</title>" >> $TMP$1.html
    echo '<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>' >> $TMP$1.html
    echo '</head>' >> $TMP$1.html
    echo '<body>' >> $TMP$1.html
    Markdown.pl --html4tags $1 >> $TMP$1.html
    echo '</body>' >> $TMP$1.html
    echo '</html>' >> $TMP$1.html
    xdg-open $TMP$1.html
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
