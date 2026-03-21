---
lang: ru-RU
title: Настройка DHCP для IPv4 и IPv6 в GNS3
subtitle: Лабораторная работа №7
author: Суннатилло Махмудов
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 25 ноября 2025

theme: metropolis
aspectratio: 169
section-titles: true
slide_level: 2

header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель лабораторной работы

## Основная цель
Получить практические навыки настройки **DHCPv4**, **DHCPv6 Stateless** и **DHCPv6 Stateful** на маршрутизаторе **VyOS** в среде GNS3.

## Что реализовано
1. Настройка DHCPv4 и автоматическое получение IPv4-адресов клиентом.  
2. Настройка IPv6 и механизмов SLAAC.  
3. Организация DHCPv6 в режимах Stateless и Stateful.  
4. Анализ трафика DHCP/ICMPv6 в Wireshark.

# Теоретическая часть

## Stateless DHCPv6
* Адрес формируется через SLAAC  
* DHCP передает только:  
  * DNS  
  * доменную зону  
  * время жизни записей

## Stateful DHCPv6
* Аналог DHCPv4  
* Сервер выделяет IPv6-адреса  
* Сообщения: Solicit → Advertise → Request → Reply

# Топология сети

![Топология IPv6-сети](09.png){ width=75% }

## VyOS как DHCPv4-сервер

![DHCPv4 конфигурация](03.png){ width=80% }

## Клиент получает IPv4-адрес

![Получение DHCP-адреса](04.png){ width=80% }

## Интерфейсы IPv6

![Настройка IPv6](10.png){ width=80% }

## DHCPv6 Stateless

![DHCPv6 Stateless](11.png){ width=80% }

## SLAAC на PC2

![IPv6 адрес SLAAC](13.png){ width=70% }

## Проверка на клиенте

![resolv.conf](15.png){ width=70% }

## DHCPv6 Stateful

![DHCPv6 Stateful](20.png){ width=80% }

## Клиент PC3 получает адрес DHCPv6

![dhclient](22.png){ width=80% }

## Проверка сети

![IPv6 настройки](23.png){ width=80% }

# Вывод

## Основные результаты
* Настроен DHCPv4 на маршрутизаторе VyOS.  
* Реализованы SLAAC, Stateless и Stateful DHCPv6.  
* Клиенты корректно получают IPv4/IPv6-адреса и сетевые параметры.  
* Wireshark подтвердил правильность обмена сообщениями DHCPv4/DHCPv6.  
* Сеть полностью функционирует в IPv4 и IPv6-окружении.
