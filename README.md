### Repro for yapf formatting issue in VSCode-Python

Demonstrates `yapf` failing to format all files within a directory when a file called `logging.py` is present.

1. Verify `Format Document` works in `mymodule/myfile?.py`. Undo the changes.
1. Rename `mymodule/_logging.py` to `mymodule/logging.py`.
1. Note `Format Document` no longer works for either of `mymodule/myfile?.py`, and there is no output in the Python output pane.
1. Verify `yapf -i mymodule/myfile1.py` still works as expected. Undo the changes.
1. Verify `yapf -ri mymodule` still works as expected. Undo the changes.
1. Note that `cd mymodule ; yapf -i myfile1.py` throws an exception: `AttributeError: module 'logging' has no attribute 'getLogger'`.

This sugguests that `yapf` fails due to VSCode-Python setting the CWD to that of the target file.

A file called `logging.py` is perfectly valid within a module's directory due to Python's import priorities. However, as soon as you `cd` into that directory you change the import priorities.
