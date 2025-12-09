# Лабораторная работа №2 - Red-Black Tree Dictionary

**Вариант:** Dict на основе Red-Black Tree

## Описание

Реализация неизменяемого словаря (dictionary) на основе красно-черного дерева на языке Clojure.

## Требования

### Функции:
- ✅ Добавление и удаление элементов
- ✅ Фильтрация
- ✅ Отображение (map)
- ✅ Свертки (левая и правая)
- ✅ Структура является моноидом

### Дополнительно:
- ✅ Структура данных неизменяемая (immutable)
- ✅ Библиотека протестирована в рамках unit testing
- ✅ Библиотека протестирована в рамках property-based тестирования (13 свойств)
- ✅ Структура полиморфна (протокол IDict)
- ✅ Реализованы стандартные протоколы Clojure
- ✅ Эффективное сравнение словарей

## Структура проекта

```
rb-dict/
├── src/rb_dict/
│   ├── api.clj      # Определение протокола IDict
│   ├── core.clj     # Публичный API
│   └── impl.clj     # Реализация красно-черного дерева
└── test/rb_dict/
    ├── generators.clj      # Генераторы для property-based тестов
    ├── property_test.clj   # Property-based тесты (13 свойств)
    └── unit_test.clj       # Unit-тесты
```

## API

```clojure
(require '[rb-dict.core :as dict])

;; Создание и работа со словарем
(def d (-> dict/empty-dict
           (dict/insert 1 "one")
           (dict/insert 2 "two")
           (dict/insert 3 "three")))

;; Основные операции
(dict/lookup d 2)           ;=> "two"
(dict/remove-key d 2)       ;=> словарь без ключа 2
(dict/dict-map d str)       ;=> применить функцию к значениям
(dict/dict-filter d pred)   ;=> отфильтровать по предикату

;; Свертки
(dict/foldl d f init)       ;=> левая свертка
(dict/foldr d f init)       ;=> правая свертка

;; Моноид
(dict/mappend d1 d2)        ;=> объединение словарей
(dict/equal? d1 d2)         ;=> сравнение

;; Стандартные протоколы Clojure
(seq d)                     ;=> (1 2 3)
(count d)                   ;=> 3
(get d 1)                   ;=> "one"
(assoc d 4 "four")          ;=> добавить элемент
(d 1)                       ;=> "one" (словарь как функция)
```

## Запуск тестов

```bash
lein test
```

Результат:
- 9 unit-тестов
- 13 property-based тестов (по 100 итераций каждый)
- Всего: 22 теста, 51+ проверка

## Зависимости

- Clojure 1.11.1
- test.check 1.1.1 (для property-based тестирования)

## Автор

ИТМО, 2025
