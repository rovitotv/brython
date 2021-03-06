Brython implements Python version 3, based on the 
[Python Language Reference](https://docs.python.org/3/reference/index.html)


The implementation takes into account the browsers limitations, in particular
those related to the file system. Writing is impossible, and reading is
limited to the folders accessible with an Ajax request.

Keywords and built-in functions
-------------------------------

Brython supports all the keywords and most functions of Python 3 :

- keywords : `as, assert, break, class, continue, def, del, elif, else,`
  `except, False, finally, for, from, global, if, import, is, lambda, `
  `None, nonlocal, pass, return, True, try, while, with, yield`
- built-in functions : `abs(), all(), any(), ascii(), bin(), bool(), bytes(),`
  `callable(), chr(), classmethod(), delattr(), dict(), dir(), divmod(), `
  `enumerate(), eval(), exec(), filter(), float(), frozenset(), getattr(), `
  `globals(), hasattr(), hash(), hex(), id(), input(), int(), isinstance(), `
  `iter(), len(), list(), locals(), map(), max(), min(), next(), object(), `
  `open(), ord(), pow(), print(), property(), range(), repr(), reversed(), `
  `round(), set(), setattr(), slice(), sorted(), str(), sum(), super(), `
  `tuple(), type(), zip(), __import__()`

By default, `print()` will output to the web browser console and so are the 
error messages. `sys.stderr` and `sys.stdout` can be assigned to an object 
with a `write()` method, and this allows for the redirection of output to go 
to a window or text area, for example.

`sys.stdin` is not implemented at this time, however there is an `input()` 
built-in function that will open a blocking input dialog (a prompt).

To open a print dialog (to a printer), call `window.print` (`window` is 
defined in module **browser**).

The built-in functions `memoryview(), vars()` are not implemented in the 
current version.

Built-in value `__name__`
-------------------------

The built-in variable `__name__` is set to the value of the attribute `id`
of the script. For instance:

```python
<script type="text/python" id="myscript">
assert __name__ == 'myscript'
</script>
```

If 2 scripts have the same `id`, an exception is raised.

For scripts that don't have an explicit `id` set :

- if no script has its `id` set to `__main__`, the first "unnamed" script has
  its `__name__` set to `__main__`. So, if there only one script in the page,
  it will be able to run the usual test :

<blockquote>
```python
<script type="text/python">
if __name__=='__main__':
    print('hello !')
</script>
```
</blockquote>

- for the other unnamed scripts, `__name__` is set to a random string starting
  with `__main__`
