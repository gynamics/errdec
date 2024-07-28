# errdec
Error code decoder.

When your last command throws an error code, what does it mean? If unfortunately you can not check it online, it may take you a little bit of time to check it out. So let's optimize that!

```sh
% sl          # an error happens if command 'sl' does not exist
% errdec $?   # check what the last error is? 
Errno Name: EKEYEXPIRED
Comments: Key has expired
Libc Info:

 -- Macro: int EKEYEXPIRED

     “Key has expired.”

```

(Hint: in bash `$?` expands to last return value, here it is 127.)

You can also check multiple errno at a time (e. g. ./errdec 123 126 127). This is a python script so make sure you have `python` installed! Besides, if you want to search it in libc document, you will need `info` command, too.

You can also modify this script for identifying error codes in a customized header.

```python

    my_err_defs = [
        'projectA/errno.h',
        'projectB/errno.h',
        'projectB/ext-errno.h',
    ]

    ec = ErrorCodeChecker(my_err_defs)
    # do one check
    ec.check(errno)
```
