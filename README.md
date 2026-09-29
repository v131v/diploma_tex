# ВКР: гибридное кодирование и репликация

Исходники выпускной квалификационной работы СПбГУ 2026 года:
«Разработка гибридной системы erasure coding и репликации на основе
температуры данных».

Оформление основано на исходном
[LaTeX-шаблоне ВКР СПбГУ](https://github.com/itonik/spbu_diploma).

Репозиторий содержит текст ВКР в LaTeX, библиографию, схемы, графики
экспериментов и текст выступления. Исходный код описанного в работе
экспериментального прототипа и генераторы графиков сюда не входят.

## Быстрый старт

```bash
git clone git@github.com:v131v/diploma_tex.git
cd diploma_tex
latexmk -pdf main.tex
```

Готовый документ появится в `build/main.pdf`.

Сборку нужно запускать из корня репозитория: документ использует относительные
пути к разделам, изображениям, стилям и библиографии.

## Что установить

Для сборки нужны:

- `pdflatex`;
- `latexmk`;
- `biber`;
- LaTeX-пакеты, включая `tempora`, `extsizes`, `babel-russian`, `tikz`,
  `algorithm2e`, `biblatex` и `biblatex-gost`.

### macOS

Установить полный набор через Homebrew:

```bash
brew install --cask mactex-no-gui
export PATH="/Library/TeX/texbin:$PATH"
```

Чтобы путь сохранялся после перезапуска терминала, добавить строку `export` в
`~/.zshrc`.

### Ubuntu и Debian

Самый простой вариант со всеми нужными пакетами:

```bash
sudo apt update
sudo apt install texlive-full
```

### Windows

Установить MiKTeX и Perl для `latexmk`:

```powershell
winget install --exact --id MiKTeX.MiKTeX
winget install --exact --id StrawberryPerl.StrawberryPerl
```

В MiKTeX Console нужно включить автоматическую установку отсутствующих
пакетов. Альтернатива — полный TeX Live for Windows.

Проверить установку:

```bash
pdflatex --version
latexmk -v
biber --version
```

## Сборка

Основной документ:

```bash
latexmk -pdf main.tex
```

`latexmkrc` настраивает pdfLaTeX, Biber и каталог `build/`. Biber запускается
автоматически, отдельно вызывать его не нужно.

Удалить вспомогательные файлы, сохранив PDF:

```bash
latexmk -c main.tex
```

Удалить все результаты сборки, включая PDF:

```bash
latexmk -C main.tex
```

Если после неудачной сборки в `build/` остались файлы:

```bash
rm -rf build
```

Старый демонстрационный документ собирается отдельно:

```bash
latexmk -pdf main_example.tex
```

## Структура

- `main.tex` — точка входа актуальной ВКР;
- `titlepage.tex` — титульный лист;
- `sections/` — разделы ВКР, TikZ-схемы и неподключенные приложения;
- `references.bib` — библиография;
- `images/experiments/` — готовые графики экспериментов;
- `spbudiploma_tempora.sty` — используемый стиль оформления;
- `latexmkrc` — настройки сборки;
- `text.md` — текст выступления по слайдам;
- `COMPLIANCE.md` — сверка оформления с требованиями;
- `requierments.pdf` — программа ГИА 2026 года (имя файла исторически содержит
  опечатку);
- `main_example.tex` и `titlepage_example.tex` — старый пример шаблона;
- `build/` — генерируемые и игнорируемые Git файлы сборки.

Основной текст подключается в `main.tex` через `\input{...}`. Для добавления
раздела достаточно создать `.tex`-файл в `sections/` и подключить его там же.

## Важные детали

- Поддерживаемый движок — pdfLaTeX. XeLaTeX и LuaLaTeX не настроены.
- Шрифт документа — `Tempora-TLF` из LaTeX-пакета `tempora`, а не системный
  Times New Roman.
- Без `biblatex-gost` документ соберется с числовым стилем библиографии, но
  оформление не будет соответствовать ГОСТ.
- `sections/abstract_ru.tex`, `sections/abstract_en.tex` и
  `sections/appendix_a.tex` сейчас не подключены в `main.tex`.
- `vkr.pdf` — сохраненный снимок документа. Актуальный результат каждой сборки
  находится в `build/main.pdf` и автоматически в `vkr.pdf` не копируется.
- Сборка не требует `--shell-escape`, Python, Graphviz, ImageMagick или
  генерации графиков.
