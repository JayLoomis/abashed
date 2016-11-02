# Handy Basics #

## Global search and replace ##
You can use grep and sed together:

```bash
grep -rl [string1] [directory] | xargs sed -i 's/[string1]/[string2]/g'
```

The grep options are pretty straightforward:

+   `-r` searches recursively with the specified directory as the root.
+   `-l` lists the files in which the term was found, but doesn't show the
    context within the file. We need this in this case because we're passing the
    output of grep to sed to do the actual changes.
    
I understand sed a bit less at present, but:

+   `-i` causes sed to edit the files in place (you could also use `--in-place`).
+   I don't really know why the 's/.../.../g' works, but it does This is an area
    for future study.

## Spell-checking all files in a directory. ##

You can check the spelling in text files with the `aspell` command (included on
Goobuntu). It is very complicated. You can't check everything in a directory with
`aspell`.

```bash
for f in $(evsite list cl NNNNNNNNN) ; do echo ${f#*/en/} ; aspell list -p ~/.aspell.en.pws < $f | sort | uniq -c ; done
```

All of the words for your personal exception list should be stored in
`~/.aspell.en.pws`, a text file that starts with a definition line:

```
personal_ws-1.1 en len
```

Where len is the number of words in the list (it won't break anything if this isn't
accurate, but it's good to keep it up to date).

Each line after the first contains a single word.
<!-- ----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8 -->
