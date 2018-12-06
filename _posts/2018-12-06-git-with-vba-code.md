---
published: true
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

Вот доработанная версия файла **pre-commit.py**

```
import os
import shutil
from oletools.olevba3 import VBA_Parser


EXCEL_FILE_EXTENSIONS = ('xlsb', 'xls', 'xlsm', 'xla', 'xlt', 'xlam',)


def parse(workbook_path):
    vba_path = workbook_path + '.vba'
    vba_parser = VBA_Parser(workbook_path)
    vba_modules = vba_parser.extract_all_macros() if vba_parser.detect_vba_macros() else []

    for _, _, _, content in vba_modules:
        decoded_content = content.decode('cp1251')
        lines = []
        if '\r\n' in decoded_content:
            lines = decoded_content.split('\r\n')
        else:
            lines = decoded_content.split('\n')
        if lines:
            name = lines[0].replace('Attribute VB_Name = ', '').strip('"')
            content = [line for line in lines[1:] if not (
                line.startswith('Attribute') and 'VB_' in line)]
            if content and content[-1] == '':
                content.pop(len(content)-1)
                lines_of_code = len(content)
                non_empty_lines_of_code = len([c for c in content if c])
                if non_empty_lines_of_code > 0:
                    if not os.path.exists(os.path.join(vba_path)):
                        os.makedirs(vba_path)
                    with open(os.path.join(vba_path, name + '.bas'), 'w', encoding='utf-8') as f:
                        f.write('\n'.join(content))


if __name__ == '__main__':
    for root, dirs, files in os.walk('.'):
        for f in dirs:
            if f.endswith('.vba'):
                shutil.rmtree(os.path.join(root, f))

        for f in files:
            if f.endswith(EXCEL_FILE_EXTENSIONS):
                parse(os.path.join(root, f))
 ```
 
 
