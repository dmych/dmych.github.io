---
{"dg-publish":true,"dg-path":"Загрузка шрифтов в CSS в Obsidian.md","permalink":"/Загрузка шрифтов в CSS в Obsidian/","updated":"2026-03-07T21:27:51.545+03:00"}
---

# Загрузка шрифтов в CSS в Obsidian

_Научился этому на примере темы obsidian_ia._
# 
Сконвертировать ttf-файлы для всех начертаний (обычно четыре: regular, italic, bold, bold italic) в текстовый файл в base64:

```bash
#!/bin/bash
# usage: ttf2css.sh FONTS
for f in $*
do
   t=${f/.ttf/.txt}
   echo "${f} >>> ${t}"
   base64 -i ${f} -o ${t}
done
```

Создать CSS-файл, в соответствующие места (см `<ТЕКСТ ЗАКОДИРОВАННОГО ШРИФТА>`) вставить строки из сконвертированных текстовых файлов, задать корректные названия шрифтов.

```css
@font-face { 
  font-family: "iA Writer Mono S";
  src: url(data:application/octet-stream;base64,<ТЕКСТ ЗАКОДИРОВАННОГО ШРИФТА>) format('truetype');
}
@font-face { 
  font-family: "iA Writer Mono S";
  font-style: italic;
  src: url(data:application/octet-stream;base64,<ТЕКСТ ЗАКОДИРОВАННОГО ШРИФТА>)  format('truetype');
}
@font-face { 
  font-family: "iA Writer Mono S";
  font-weight: bold;
  src: url(data:application/octet-stream;base64,<ТЕКСТ ЗАКОДИРОВАННОГО ШРИФТА>) format('truetype');
}
@font-face { 
  font-family: "iA Writer Mono S";
  font-weight: bold;
  font-style: italic;
  src: url(data:application/octet-stream;base64,<ТЕКСТ ЗАКОДИРОВАННОГО ШРИФТА>) format('truetype');
}
```

Положить CSS-файл в папку `<VAULT>/.obsidian/snippets`, включить этот сниппет в настройках Obsidian и ввести имя шрифта в Settings/Appearance/Font.