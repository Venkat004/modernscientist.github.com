# Importing IPython Notebooks in a Pelican Blog

2013/06/02

These setup notes are based on an installation of the following:

* IPython, version 0.13.2
* nbcovert, GitHub commit [0fababc961cbe0b58df4cf0286e6b2c41fb695c5](https://github.com/ipython/nbconvert/commit/0fababc961cbe0b58df4cf0286e6b2c41fb695c5)
* liquid tags, GitHub [pull request](https://github.com/getpelican/pelican-plugins/pull/21)

------------------

The following changes were made to files due to issues discovered in the conversion process:

1. In the file `notebook.py` in the liquid tags plugin, `ConverterBloggerHTML(nb_path)` must be changed to `ConverterBloggerHTML(infile=nb_path)` on line 182 of this file, as discovered by [Thomas Wiecki](https://mobile.twitter.com/TWiecki/status/336847153374838784). 
2. Remove two lines (144-145) in the same file because they were incorrectly raising an error:

```python
if div_start not in [len(body_lines), len(body_lines) - 1]:  
    raise ValueError("parsing error: didn't find the end of the div")```  

3. The stable branch of IPython does not include a file necessary to generate the CSS styles for the notebook. To remedy this, I copied the file `$PYTHONSITE/IPython/frontend/html/notebook/static/css/notebook.css`, where `$PYTHONSITE` is the location of the python site-package directory, to `style.min.css` within the same directory.
4. To make the notebook portion of the posts inherit font styling from the article, line 24 of `style.min.css` was changed from  

```body{margin:0;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:13px;line-height:2 px;color:#000000;background-color:#ffffff;}```

to

```body{font: inherit; font-size: inherit; background-color: inherit; font-family: inherit;} a{color:#0088cc;text-decoration:none;}```





