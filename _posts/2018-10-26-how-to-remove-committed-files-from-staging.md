---
published: true
---
## Есть как минимум два типа файлов для git: которые добавлены в гит и уже закоммичены, или те, которые добавили, но нужно сделать reset данного файла.

### Что делаем?
#### В случае с закоммиченными файлами, убираем их следующим образом:

```
# Remove the file from the repository
git rm --cached .idea/

# now update your gitignore file to ignore this folder
echo '.idea' >> .gitignore

# add the .gitignore file
git add .gitignore

git commit -m "Removed .idea files"
git push origin <branch>
```

#### В случае с добавленным файлом, но ни разу не коммиченным, то делаем так:
```
git reset <file>
```
