---
## Front matter
title: "Отчёт по лабораторной работе 1"
subtitle: "Методы кодирования и модуляция сигналов"
author: "Суннатилло Махмудов"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучение методов кодирования и модуляции сигналов с помощью языка Octave. Определение спектра и параметров сигнала. Демонстрация амплитудной модуляции и исследование свойства самосинхронизации.

# Теоретические сведения

1. **Сигналы и спектры.** Сигнал можно представить как комбинацию гармоник. Для анализа используется преобразование Фурье.
2. **Модуляция.** Изменение амплитуды, частоты или фазы несущей по закону информационного сигнала. В работе рассматривается амплитудная модуляция.
3. **Кодирование сигнала.** Способы отображения битов на электрические импульсы (NRZ, RZ, AMI, Манчестер и др.). Некоторые коды обладают свойством самосинхронизации.

# Выполнение лабораторной работы

## 1. Построение графиков в Octave

- Реализован сценарий `plot_sin.m` для построения функции:

$$y = \sin x + \frac{1}{3} \sin 3x + \frac{1}{5} \sin 5x$$

- Добавлен второй график для функции:

$$y = \cos x + \frac{1}{3} \cos 3x + \frac{1}{5} \cos 5x$$

- Экспорт графиков в PNG/EPS.

![График функции синуса](files/plot-sin.png){ #fig:001 width=80% }

![Графики синуса и косинуса](files/plot-sin-cos.png){ #fig:002 width=80% }

## 2. Разложение импульсного сигнала в ряд Фурье

- Создан сценарий `meandr.m`.
- Построены меандры с различным числом гармоник (N=2,4,6,8).
- Использованы только нечётные гармоники.

![Меандры с разным числом гармоник](files/meandr.png){ #fig:003 width=80% }

![Меандры (альтернативный вариант)](files/meandr2.png){ #fig:004 width=80% }

## 3. Определение спектра сигналов

- Построены два сигнала разной частоты (10 Гц и 40 Гц) и их спектры.
- Найден спектр их суммы.

![Сигналы](files/signal/am.png){ #fig:005 width=70% }

![Спектры сигналов](files/spectre/ami.png){ #fig:006 width=70% }

![Спектр суммы](files/spectre/bipolarrz.png){ #fig:007 width=70% }

## 4. Амплитудная модуляция

- Сгенерирован сигнал амплитудной модуляции (несущая 50 Гц, модулирующий сигнал 5 Гц).
- Построена огибающая и рассчитан спектр.

![Амплитудная модуляция](files/signal/am.png){ #fig:008 width=70% }

![Спектр АМ-сигнала](files/spectre/am.png){ #fig:009 width=70% }

## 5. Кодирование сигнала и самосинхронизация

- Проверены свойства кодов: NRZ, RZ, AMI, Манчестер, дифференциальный Манчестер.

- Получены спектры закодированных сигналов.

Примеры:

![AMI кодирование](files/signal/ami.png){ #fig:010 width=70% }

![NRZ кодирование](files/signal/bipolarnrz.png){ #fig:011 width=70% }

![RZ кодирование](files/signal/bipolarrz.png){ #fig:012 width=70% }

![Дифференциальный Манчестер](files/signal/diffmanc.png){ #fig:013 width=70% }

![Самосинхронизация (AMI)](files/sync/ami.png){ #fig:014 width=70% }

![Самосинхронизация (Манчестер)](files/sync/manchester.png){ #fig:015 width=70% }

# Вывод

В ходе работы были изучены методы анализа и обработки сигналов: построение графиков, разложение в ряд Фурье, спектральный анализ, амплитудная модуляция и кодирование сигналов. Получены навыки работы в Octave и закреплены базовые понятия теории сигналов.

# Список литературы

1. Королькова А. В., Кулябов Д. С. *Сетевые технологии. Лабораторный практикум*. — М.: РУДН, 2020.
2. Oppenheim A. V., Schafer R. W. *Discrete-Time Signal Processing*. — Prentice Hall, 2010.
3. Proakis J. G. *Digital Communications*. — McGraw-Hill, 2001.
