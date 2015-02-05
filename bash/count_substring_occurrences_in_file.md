You may need to count a string occurrences in file.

If you solution look like:

```bash
grep -c 'string' file.txt
```

You do it wrong!

Grep counting a lines, not string occurrence. If you string be twice on one line ```grep -c``` count two or more occurrence in line as one.

The right way:

```bash
grep -o 'string' file.txt | wc -l
```

It's output every matched parts on separate line, next count this lines.