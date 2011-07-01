Introduction
============

A django app (currently an idea) that compiles your css (from less, sass, etc) and js (from coffee script) when needed, and compress them.

It will have meaninful defaults and should be as flexible as possible, giving the oportunity not to use the default behavior.

Ideas
=====

General Stuff
-------------

It will use 'data-pkg' atributes to define non default behaviors to the script and link tags.
All these attributes are going to be removed after being processed on non-debug mode.

It should be able to compile js files
-------------------------------------

If the script tag contains a source with extensions other than '.js', it will try to compile the file according to the registered compiler (also known as transpiler) for that extension. Optionaly an attribute on the script tag will define the compiler.

Examples:

''' html
<script src="source.cs"></scrip>
'''

will output:

''' html
<script src="/some/defined/path/compiled.js"></scrip>
'''

2:

''' html
<script data-pkg-compiler="coffee-script" src="source.js"></scrip>
'''

will output:

''' html
<script src="/some/defined/path/compiled.js"></scrip>
'''

It should be able to compile css files
--------------------------------------

If the link tag contains a source with extensions other than '.css', it will try to compile the file according to the registered compiler (also known as transpiler) for that extension. Optionaly an attribute on the link tag will define the compiler.

Examples:

''' html
<link rel="stylesheet" href="source.less" />
'''

will output:

''' html
<link rel="stylesheet" href="/some/defined/path/compiled.css" />
'''

2:

''' html
<link rel="stylesheet" data-pkg-compiler="less" href="source.css" />
'''

will output:

''' html
<link rel="stylesheet" href="/some/defined/path/compiled.css" />
'''

It should be able to concatenate and compress css and js files
--------------------------------------------------------------

It will receive input from a defined event that can be registered by apps
-------------------------------------------------------------------------

Instaled apps will be able to register an event and print script tags that will get included into a default packager block, if found on the document.

It should be able to identify duplicate scripts
-----------------------------------------------

The script tags can include a 'data-pkg-id' attribute that will make possible to detect duplicated scripts.
Scripts without that attribute but with the exact same path will be considered duplicate too.
Optionaly, a hash can be generated from each file to detect same files with different paths.
when a duplicate is detected only the first, in document order, will be included.

A resource should be able to redefine any default behavior
----------------------------------------------------------

By using the 'data-pkg' attributes, the resources will be able to define it's specific behaviors, like changing its compiler.

It should log warnings
----------------------

It should log warnings, like:
* "The script 'x' is an external file and won't be compressed"
*

It will use the python logging module.

It may be able to manage script dependency using a defined dependency manager (it wont implement one)
-----------------------------------------------------------------------------------------------------

List of dependency managers:
* mootools's packager
*

Example of use
==============

''' html
{% package %}
{% endpackage %}
'''

Credits and inspiration
========================

* http://ryanbigg.com/guides/asset_pipeline.html
* http://blog.nodeta.com/2011/06/14/rails-3-1-asset-pipeline-in-the-real-world/
* http://documentcloud.github.com/jammit/
* http://getsprockets.org/
* https://github.com/dziegler/django-css
* https://github.com/jezdez/django_compressor

