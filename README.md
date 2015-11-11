# yolo
Yolo lets you annotate blocks of code with **machine readable** comment based **apologies**.


Why apologize in your source code?
--------
> We will encourage you to develop the three great virtues of a programmer: [laziness, impatience, and hubris.](http://c2.com/cgi/wiki?LazinessImpatienceHubris) -- LarryWall

* You only live once, that means sometimes you have to leave code in a less than desirable state.
* Larry Wall's third virtue should make you want to apologize when and where this happens. 



What does a machine readable apology get me?
--------
This is a new project, it aims to be a core library that enables other interesting little tools.There are lots of directions this can be taken, some ideas include:

* A git badge that displays what % of your codebase is yoloed
* A sublime text/vim/emacs plugin that tints, highlights, dims, and/or disables linters in a yolo block
* Automated issue/todo generation
* Other things

Ideas are great, but I needed an actual consumer to drive the initial implementation:

* Git blame based forgiveness and shaming

The proof of concept first usage of yolo is a git blame integration that aims to enable shaming and temporary forgiveness (with expiration dates) of yoloed code. As a first step and building block the yolo + git blame integration generates a json report that combines the line by line metadata generated by the each utility.

You can see this in action here in [the yolo.py file](https://github.com/TomNeyland/yolo/blob/master/yolo/yolo.py#L157-L170), and the [json report](https://github.com/TomNeyland/yolo/blob/master/yolo_example.json#L1423-L1693).


Command line usage
--------
```shell
# install after cloning the repo (since this is no on pypy yet)
pip install -e . -U

# run yolo on some files
yolo myfile.py yolo/yolo.py

# ask yolo for help
yolo --help

# usage: yolo [-h] [-c CONFIG] [--repo REPO] sourcefiles [sourcefiles ...]

# Args that start with '--' (eg. --repo) can also be set in a config file
# (./.yolorc or specified via -c). The recognized syntax for setting (key,
# value) pairs is based on the INI and YAML formats (e.g. key=value or
# foo=TRUE). For full documentation of the differences from the standards please
# refer to the ConfigArgParse documentation. If an arg is specified in more than
# one place, then commandline values override environment variables which
# override config file values which override defaults.

# positional arguments:
#   sourcefiles           the sourcefile(s) to run yolo on

# optional arguments:
#   -h, --help            show this help message and exit
#   -c CONFIG, --config CONFIG
#                         config file path [env var: YOLO_CONFIG]
#   --repo REPO           the git repo running yolo on
```


Python usage
--------
```python
from yolo import yolo, yolo_file

# run yolo on a string
my_source_code = 'pretend this is some python code'
yolo_result = yolo(my_source_code)

# run yolo on a file
yolo_result = yolo_file('something.py')
```
