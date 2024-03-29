CWiki
=====

CWiki is a Vim filetype plugin that allows to create single file wiki with unobtrusive syntax. It enhances syntax/folding/mappings of the current buffer, converting it to simple yet useful offline wiki. Name stands for something like "compact wiki". Here is a screenshot:

![Screenshot](http://a-hw.narod.ru/cwiki.png "Screenshot")

Features
-------- 

* single file storage (readable textual format; built-in Vim encryption can be applied) 
* unobtrusive wikiwords (no special symbols like brackets) 
* synonyms (you can define them, so "Bill", "William", and "Mr. W. Smith" point to the same article) 
* folding (separates articles; shows number of meaningful article lines) 
* syntax highlighting 
* visual wikiword selector 

Syntax 
------

Article titles, first, second, and thrird levels (level affects folding only, no other side effects):

```
+++ Wiki word
++++ Wiki word
+++++ Wiki word
```

Optional metadata is expected to be the first non-blank line after the title: 

```
    Synonyms: a, b, {C,c}def
```

Whitespace before "Synonyms" and after comma is mandatory. Curly braces are expanded like shell patterns, i.e. the line above is equivalent to the following: 

```
    Synonyms: a, b, Cdef, cdef
```

Actually "Synonyms" is the only metadata currently supported.

Sample CWiki file
-----------------

Here is minimal yet complete sample of the wikifile. Just paste it into new buffer and type :set ft=cwiki (after installing the plugin, of course). 

```
+++ First article 

    Synonyms: 1st article, {A,a}rticle #1 

Here we have some text. I'd like to mention Mr. W. 
Smith (note that his name is wrapped with <CR>). 

+++ Mr. W. Smith 

    Synonyms: William, Bill, dad 

This article is about Mr. W. Smith, also known as 
William, Bill. He has two doughters: Jane and Kim. 

Article #1 mentions Bill. Though, that 1st article 
is rather short. 

++++ Jane Smith 

    Synonyms: Jane 

Ms. Jane's dad is Bill. 

++++ Kim 

Kim is too young, so we refer to her without the last 
name, e.g. no synonyms yet. She loves her dad. 
```

Key mappings 
------------

* `n_Ctrl-]`: follow wikiword under cursor 
* `v_Ctrl-]`: add new article; currently selected text is used as title 
* `n_F5`: refresh the wiki (you need this if you altered synonyms) 
* `n_F3`: show wikiword selector (current wikiword will be highlighted; move cursor to the desired wikiword and press <CR> to select it, or press <F3> to close the selector) 

No other special bindings so far. You can move text around at will. Specifically it is really handy to move whole articles by doing `DD` and `p` with folded blocks. 

Highlighting groups
-------------------

In case you want to override colors, here are highlighting groups used by CWiki:

* `CWikiTitle1`, `CWikiTitle2`, `CWikiTitle3`: article titles (linked to Title by default)
* `CWikiTitleMark`: "+" signs in the title (linked to Title by default)
* `CWikiWord`: any detected wikiword (linked to Underlined by default)

Windows specific hints 
----------------------

AFAIK on Win32 by default Underlined looks like Normal, so you won't be able to see any wikiwords. The following might help: 

```
:highlight Underlined gui=underlined
```

Safety measures
---------------

I didn't experience any problems with the plugin yet. But maybe it is a good idea to make backups every now and then (if you do something useful, of course): 

```
set backup 
set writebackup 
au BufWritePre <buffer> let &bex = '-' . strftime("%Y%b%d%X") . '~'
```

Installing
----------

Any typical install pocedure like copying the file into your ~/.vim/ftplugin/ directory or using Vundle will work.

To enable CWiki for currently loaded file do the following:

```
:set ft=cwiki
```

You might want to add an autocommand. Alternatively, you can add modeline to your wikifile: 

```
vim: ft=cwiki
```

Links
-----

This plugin also can be found at www.vim.org:

http://www.vim.org/scripts/script.php?script_id=2176
