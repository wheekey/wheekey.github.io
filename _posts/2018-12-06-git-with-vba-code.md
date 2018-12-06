---
published: false
---
## A New Post

[Инструкция](https://www.xltrail.com/blog/auto-export-vba-commit-hook "Инструкция")

Чтобы нормально преобразовывались файлы, нужно указать кодировку.

**A rule of thumb is: Always use Unicode internally. Decode what you receive, and encode what you send.**

# -*- coding: utf-8 -*-
print u"åäö".encode('utf-8')
Another didactic example is a Python program to convert between ISO-8859-1 and UTF-8, making everything uppercase in between.

```
import sys
for line in sys.stdin:
    # Decode what you receive:
    line = line.decode('iso8859-1')

    # Work with Unicode internally:
    line = line.upper()

    # Encode what you send:
    line = line.encode('utf-8')
    sys.stdout.write(line)
```

Вот доработанная версия файлаp