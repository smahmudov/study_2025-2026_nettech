---
## Front matter
title: "Отчёт по лабораторной работе 4"
subtitle: "Подготовка экспериментального стенда GNS3"
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

Установка и настройка GNS3 и сопутствующего программного обеспечения.

# Теоретические сведения по работе

**GNS3 (Graphical Network Simulator 3)** — это программная среда для моделирования и тестирования сетей различной сложности.  
Она позволяет создавать виртуальные топологии, включающие маршрутизаторы, коммутаторы, серверы и пользовательские узлы, а также объединять их с реальными устройствами.  
GNS3 широко используется в учебных и исследовательских целях, а также при подготовке к сертификациям (например, Cisco CCNA/CCNP).

## Архитектура GNS3

Архитектура GNS3 состоит из двух основных компонентов:

1. **GNS3 GUI (Graphical User Interface)** — графический интерфейс, установленный на основной операционной системе пользователя.  
   Он отвечает за визуальное проектирование топологий, настройку устройств и взаимодействие с серверной частью.

2. **GNS3 Server (или GNS3 VM)** — серверная часть, которая выполняет все вычисления, эмуляцию и обработку трафика.  
   Она разворачивается как виртуальная машина в средах **VMware** или **VirtualBox** и взаимодействует с клиентом через REST API.  

Связь между клиентом и сервером осуществляется по протоколам **HTTP/HTTPS** и **Telnet/SSH**.  

## Эмуляция устройств

GNS3 поддерживает несколько типов виртуальных устройств:

- **QEMU** — универсальный эмулятор, позволяющий запускать полноценные образы Linux-систем (например, FRR, VyOS, pfSense);  
- **Dynamips** — эмулятор маршрутизаторов Cisco старых серий (2600, 3700 и др.);  
- **IOU/IOSv** — эмуляторы современных Cisco IOS на основе виртуализации;  
- **VPCS** — лёгкие виртуальные клиенты, позволяющие генерировать пинг и тестировать связность сети.

## FRRouting (FRR)

**FRRouting (FRR)** — это набор протоколов динамической маршрутизации с открытым исходным кодом, совместимый с Cisco и Juniper.  
FRR поддерживает такие протоколы, как **OSPF**, **BGP**, **RIP**, **IS-IS** и **PIM**.  
Благодаря лёгкости и стабильности FRR часто используется в образовательных стендах и для построения виртуальных маршрутизаторов в GNS3.

## VyOS

**VyOS** — дистрибутив Linux, предназначенный для реализации функционала маршрутизатора, брандмауэра и VPN-шлюза.  
Он основан на Debian и использует интерфейс команд в стиле **JunOS**.  
VyOS может устанавливаться на физическое оборудование, в виртуальные среды или облачные платформы (AWS, Azure, Proxmox).  
В GNS3 образ VyOS используется для моделирования сетевых маршрутов и VPN-соединений.

# Выполнение лабораторной работы

## Запуск GNS3 VM и подключение к серверу

1. В ходе выполнения лабораторной работы для запуска **GNS3 VM** была использована платформа **VMware**.  
   Это связано с тем, что при использовании **VirtualBox** наблюдались сбои в работе (вылеты виртуальной машины), поэтому для стабильности была выбрана среда VMware.  
   ![Сбой VirtualBox](0.png){ #fig:000 width=80% }

   После запуска виртуальной машины **GNS3 VM** отобразились параметры сервера:  
   – версия GNS3: **3.0.5**;  
   – гипервизор: **VMware**;  
   – поддержка KVM: **True**;  
   – IP-адрес сервера: `192.168.133.129`, порт: `80`.  
   Также указаны данные для подключения по **SSH** и **Web-UI**.  

   ![Информация о GNS3 сервере](01.png){ #fig:001 width=80% }

2. В основном приложении **GNS3** был запущен мастер настройки (**Setup Wizard**).  
   На этапе подключения к удалённому контроллеру введены следующие параметры:  
   – **Protocol:** HTTP;  
   – **Host:** `192.168.133.129`;  
   – **Port:** `80 TCP`;  
   – **Username:** admin;  
   – **Password:** *****.  

   ![Настройка подключения к удалённому контроллеру GNS3](02.png){ #fig:002 width=80% }

## Добавление образа маршрутизатора FRRouting (FRR)

3. В мастере установки устройств был выбран образ **FRR version 8.1.0**, отмеченный как *Ready to install*.  
   Образ найден локально и подготовлен к установке.  

   ![Выбор версии FRR для установки](03.png){ #fig:003 width=80% }

4. В окне **QEMU VM template configuration** заданы параметры виртуального устройства:  
   – имя шаблона: **FRR**;  
   – категория: **Routers**;  
   – объем оперативной памяти: **256 MB**;  
   – количество vCPU: **1**;  
   – платформа QEMU: **x86_64**;  
   – при завершении: *Send the shutdown signal (ACPI)*;  
   – тип консоли: **telnet**.  

   ![Настройки шаблона FRR в GNS3](04.png){ #fig:004 width=80% }

5. После запуска виртуального устройства через **PuTTY** был выполнен вход в систему.  
   В консоли отобразилось приветственное сообщение **Alpine Linux** и информация о запущенном сервисе **FRRouting (version 8.1)**.  

   ![Запуск виртуального маршрутизатора FRR](05.png){ #fig:005 width=80% }

## Добавление образа маршрутизатора VyOS

6. Аналогично был добавлен образ маршрутизатора **VyOS**.  
   В списке доступных версий выбрана **VyOS version 1.3.3-qemu**, статус — *Found locally*.  

   ![Выбор образа VyOS для установки](06.png){ #fig:006 width=80% }

7. После запуска устройства **VyOS** через консоль **PuTTY** появилось приглашение к входу в систему, что подтверждает успешную установку и корректную загрузку виртуальной машины.  

   ![Запуск виртуального маршрутизатора VyOS](07.png){ #fig:007 width=80% }

# Вывод

В ходе выполнения лабораторной работы была развернута виртуальная среда **GNS3** на базе **VMware**, успешно добавлены и запущены образы маршрутизаторов **FRRouting (FRR)** и **VyOS**.  
