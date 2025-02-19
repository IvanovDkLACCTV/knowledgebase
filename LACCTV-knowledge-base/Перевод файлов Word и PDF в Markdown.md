


---

#### 🔄 1. Онлайн-конвертеры:

- [word2md.com](https://word2md.com/)
- cloudconvert.com
- pandoc.org/try

Обычно достаточно загрузить файл `.docx` или `.pdf` → выбрать формат вывода **Markdown** → скачать `.md` файл.

---

#### 🛠 2. Программа **Pandoc** (локально):

Если хочется более гибкий инструмент:

1. Скачай Pandoc: pandoc.org
2. Открой терминал и выполни:
    
    ```bash
    
    pandoc файл.docx -o файл.md
```
    
    Или для PDF (может быть хуже распознано):
    
    ```bash
    
    pandoc файл.pdf -o файл.md
    ```
    

> Pandoc – мощная штука, часто её используют для автоматизации.

#### 🧑‍💻 3. В Obsidian — Плагины для импорта:

- **Markdown Importer** – помогает загружать `.docx`, `.html` и другие форматы прямо в Obsidian.
    - Установка: `Settings → Community Plugins → Browse → Markdown Importer`.
    - После установки будет кнопка `Import` в панели.