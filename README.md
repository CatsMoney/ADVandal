<div align="center">

# ⚡ ADVandal

**Продвинутый перехват и уничтожение скрытых рекламных скриптов Яндекса на этапе инициализации.**

[![GitHub license](https://img.shields.io/github/license/XPay-Company/ADVandal?style=for-the-badge&color=orange)](https://github.com/XPay-Company/ADVandal/blob/main/LICENSE)
[![uBlock Origin](https://img.shields.io/badge/uBlock%20Origin-Compatible-purple?style=for-the-badge&logo=ublockorigin)](https://github.com/gorhill/uBlock)
[![Stage](https://img.shields.io/badge/Stage-Development-blue?style=for-the-badge)](https://github.com/XPay-Company/ADVandal)

*«Use ADVandal if you want to live normally!»*

---
<p align="left">
  Обычные косметические фильтры скрывают последствия рекламы (уже загруженные баннеры). 
  <b>ADVandal работает иначе:</b> он внедрится в коллектив скриптов сайта на этапе <code>document-start</code>, замаскируется под системные объекты и сломает цепочку вызовов функций (например, <code>b.load</code> и <code>b._formatImage</code>) до того, как браузер отправит запрос за картинкой.
</p>

</div>

---

## 🚀 Как это работает (Под капотом)
Проект использует технику **Monkey-patching** (динамическая подмена методов «на лету»):
1. **Ранний запуск:** Скриптлет инициализируется uBlock Origin раньше, чем выполняются родные скрипты страницы.
2. **Перехват конструкторов:** Мы переопределяем свойства глобального объекта `window`, отслеживая создание рекламных модулей Яндекса.
3. **Глушение сетевой активности:** Оригинальные функции отправки запросов заменяются на пустые заглушки (`noopFunc`), полностью обрывая стек вызовов. Трафик не расходуется, баннеры не собираются.

---

## 🛠 Инструкция по установке

### Шаг 1. Подключение скриптлета в uBlock Origin
1. Откройте **Дашборд uBlock Origin** -> вкладка **Настройки**.
2. В самом низу активируйте галочку **«Я продвинутый пользователь»** и нажмите появившиеся шестерёнки.
3. Найдите параметр `userResourcesLocation` и замените его значение на прямую ссылку к нашему скрипту:
```text
   userResourcesLocation [https://raw.githubusercontent.com/XPay-Company/ADVandal/main/src/advandal.js](https://raw.githubusercontent.com/XPay-Company/ADVandal/main/src/advandal.js)
