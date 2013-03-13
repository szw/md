#!/bin/bash
DIRNAME=`dirname "$1"`
BASENAME=`basename "$1"`
TMP=/tmp/md_view_tmp.html

if [ -z "$2" ]; then
    TARGET=$TMP
else
    TARGET="$2"
fi

function run_md {
    rm -f $TARGET
    echo '<!DOCTYPE html>' > $TARGET
    echo '<html lang="en"' >> $TARGET
    echo '<head>' >> $TARGET
    echo '<meta charset="utf-8" />' >> $TARGET
    echo "<title>$1 - Markdown Preview Window</title>" >> $TARGET
    echo "<style>" >> $TARGET
    echo "/* Github Markdown CSS by Andy Ferra: https://gist.github.com/andyferra/2554919 */" >> $TARGET
    echo "body { font-family: Helvetica, arial, sans-serif; font-size: 14px; line-height: 1.6; padding-top: 10px; padding-bottom: 10px; background-color: white; padding: 30px; }" >> $TARGET
    echo "body > *:first-child { margin-top: 0 !important; }" >> $TARGET
    echo "body > *:last-child { margin-bottom: 0 !important; }" >> $TARGET
    echo "a { color: #4183C4; }" >> $TARGET
    echo "a.absent { color: #cc0000; }" >> $TARGET
    echo "a.anchor { display: block; padding-left: 30px; margin-left: -30px; cursor: pointer; position: absolute; top: 0; left: 0; bottom: 0; }" >> $TARGET
    echo "h1, h2, h3, h4, h5, h6 { margin: 20px 0 10px; padding: 0; font-weight: bold; -webkit-font-smoothing: antialiased; cursor: text; position: relative; }" >> $TARGET
    echo "h1:hover a.anchor, h2:hover a.anchor, h3:hover a.anchor, h4:hover a.anchor, h5:hover a.anchor, h6:hover a.anchor { text-decoration: none; }" >> $TARGET
    echo "h1 tt, h1 code { font-size: inherit; }" >> $TARGET
    echo "h2 tt, h2 code { font-size: inherit; }" >> $TARGET
    echo "h3 tt, h3 code { font-size: inherit; }" >> $TARGET
    echo "h4 tt, h4 code { font-size: inherit; }" >> $TARGET
    echo "h5 tt, h5 code { font-size: inherit; }" >> $TARGET
    echo "h6 tt, h6 code { font-size: inherit; }" >> $TARGET
    echo "h1 { font-size: 28px; color: black; }" >> $TARGET
    echo "h2 { font-size: 24px; border-bottom: 1px solid #cccccc; color: black; }" >> $TARGET
    echo "h3 { font-size: 18px; }" >> $TARGET
    echo "h4 { font-size: 16px; }" >> $TARGET
    echo "h5 { font-size: 14px; }" >> $TARGET
    echo "h6 { color: #777777; font-size: 14px; }" >> $TARGET
    echo "p, blockquote, ul, ol, dl, li, table, pre { margin: 15px 0; }" >> $TARGET
    echo "hr { border: 0 none; color: #cccccc; height: 4px; padding: 0; }" >> $TARGET
    echo "body > h2:first-child { margin-top: 0; padding-top: 0; }" >> $TARGET
    echo "body > h1:first-child { margin-top: 0; padding-top: 0; }" >> $TARGET
    echo "body > h1:first-child + h2 { margin-top: 0; padding-top: 0; }" >> $TARGET
    echo "body > h3:first-child, body > h4:first-child, body > h5:first-child, body > h6:first-child { margin-top: 0; padding-top: 0; }" >> $TARGET
    echo "a:first-child h1, a:first-child h2, a:first-child h3, a:first-child h4, a:first-child h5, a:first-child h6 { margin-top: 0; padding-top: 0; }" >> $TARGET
    echo "h1 p, h2 p, h3 p, h4 p, h5 p, h6 p { margin-top: 0; }" >> $TARGET
    echo "li p.first { display: inline-block; }" >> $TARGET
    echo "ul, ol { padding-left: 30px; }" >> $TARGET
    echo "ul :first-child, ol :first-child { margin-top: 0; }" >> $TARGET
    echo "ul :last-child, ol :last-child { margin-bottom: 0; }" >> $TARGET
    echo "dl { padding: 0; }" >> $TARGET
    echo "dl dt { font-size: 14px; font-weight: bold; font-style: italic; padding: 0; margin: 15px 0 5px; }" >> $TARGET
    echo "dl dt:first-child { padding: 0; }" >> $TARGET
    echo "dl dt > :first-child { margin-top: 0; }" >> $TARGET
    echo "dl dt > :last-child { margin-bottom: 0; }" >> $TARGET
    echo "dl dd { margin: 0 0 15px; padding: 0 15px; }" >> $TARGET
    echo "dl dd > :first-child { margin-top: 0; }" >> $TARGET
    echo "dl dd > :last-child { margin-bottom: 0; }" >> $TARGET
    echo "blockquote { border-left: 4px solid #dddddd; padding: 0 15px; color: #777777; }" >> $TARGET
    echo "blockquote > :first-child { margin-top: 0; }" >> $TARGET
    echo "blockquote > :last-child { margin-bottom: 0; }" >> $TARGET
    echo "table { padding: 0; }" >> $TARGET
    echo "table tr { border-top: 1px solid #cccccc; background-color: white; margin: 0; padding: 0; }" >> $TARGET
    echo "table tr:nth-child(2n) { background-color: #f8f8f8; }" >> $TARGET
    echo "table tr th { font-weight: bold; border: 1px solid #cccccc; text-align: left; margin: 0; padding: 6px 13px; }" >> $TARGET
    echo "table tr td { border: 1px solid #cccccc; text-align: left; margin: 0; padding: 6px 13px; }" >> $TARGET
    echo "table tr th :first-child, table tr td :first-child { margin-top: 0; }" >> $TARGET
    echo "table tr th :last-child, table tr td :last-child { margin-bottom: 0; }" >> $TARGET
    echo "img { max-width: 100%; }" >> $TARGET
    echo "span.frame { display: block; overflow: hidden; }" >> $TARGET
    echo "span.frame > span { border: 1px solid #dddddd; display: block; float: left; overflow: hidden; margin: 13px 0 0; padding: 7px; width: auto; }" >> $TARGET
    echo "span.frame span img { display: block; float: left; }" >> $TARGET
    echo "span.frame span span { clear: both; color: #333333; display: block; padding: 5px 0 0; }" >> $TARGET
    echo "span.align-center { display: block; overflow: hidden; clear: both; }" >> $TARGET
    echo "span.align-center > span { display: block; overflow: hidden; margin: 13px auto 0; text-align: center; }" >> $TARGET
    echo "span.align-center span img { margin: 0 auto; text-align: center; }" >> $TARGET
    echo "span.align-right { display: block; overflow: hidden; clear: both; }" >> $TARGET
    echo "span.align-right > span { display: block; overflow: hidden; margin: 13px 0 0; text-align: right; }" >> $TARGET
    echo "span.align-right span img { margin: 0; text-align: right; }" >> $TARGET
    echo "span.float-left { display: block; margin-right: 13px; overflow: hidden; float: left; }" >> $TARGET
    echo "span.float-left span { margin: 13px 0 0; }" >> $TARGET
    echo "span.float-right { display: block; margin-left: 13px; overflow: hidden; float: right; }" >> $TARGET
    echo "span.float-right > span { display: block; overflow: hidden; margin: 13px auto 0; text-align: right; }" >> $TARGET
    echo "code, tt { margin: 0 2px; padding: 0 5px; white-space: nowrap; border: 1px solid #eaeaea; background-color: #f8f8f8; border-radius: 3px; }" >> $TARGET
    echo "pre code { margin: 0; padding: 0; white-space: pre; border: none; background: transparent; }" >> $TARGET
    echo ".highlight pre { background-color: #f8f8f8; border: 1px solid #cccccc; font-size: 13px; line-height: 19px; overflow: auto; padding: 6px 10px; border-radius: 3px; }" >> $TARGET
    echo "pre { background-color: #f8f8f8; border: 1px solid #cccccc; font-size: 13px; line-height: 19px; overflow: auto; padding: 6px 10px; border-radius: 3px; }" >> $TARGET
    echo "pre code, pre tt { background-color: transparent; border: none; }" >> $TARGET
    echo "</style>" >> $TARGET
    echo '</head>' >> $TARGET
    echo '<body>' >> $TARGET
    cd "$DIRNAME"
    Markdown.pl --html4tags "$BASENAME" >> $TARGET
    echo '</body>' >> $TARGET
    echo '</html>' >> $TARGET
    if [ $TARGET = $TMP ]; then
        if [ $(uname -s) = "Darwin" ]; then
            open $TARGET
        else
            xdg-open $TARGET
        fi
    fi
}

function usage {
    echo -e "MD - The Markdown Viewer 0.2 - Copyright (c) 2012-2013 Szymon Wrozynski"
    echo -e "Licensed under the MIT License. More details here: https://github.com/szw/md"
    echo -e "Usage: $0 [file_name [target_name]]"
}

if [ -z "$1" ]; then
    usage
else
    run_md
fi
