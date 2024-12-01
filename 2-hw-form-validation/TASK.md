# Задание: Создание формы профиля пользователя

## Описание
После реализации формы регистрации необходимо добавить форму редактирования профиля пользователя. Это типичный сценарий для многих приложений, где пользователь может изменить свои данные после регистрации.

## Структура проекта
```
src/
  components/
    RegisterForm.svelte  (существующий компонент)
    ProfileForm.svelte   (новый компонент)
  App.svelte            (обновить для отображения обеих форм)
```

## Требования

### 1. Создать компонент ProfileForm
- Создайте новый компонент `ProfileForm.svelte` в директории `src/components`
- Форма должна содержать следующие поля:
  
  Базовые поля (как в регистрации):
  - Username (имя пользователя)
  - Password (текущий пароль)
  - New Password (новый пароль)
  
  Дополнительные поля профиля:
  - Full Name (полное имя, два слова)
  - Age (возраст, число от 18 до 100)
  - Bio (краткая биография, от 10 до 200 символов)
  - Email (корректный email адрес)
  - Phone (телефонный номер в формате +7XXXXXXXXXX)

### 2. Валидация полей
- Применить базовые правила валидации для полей из формы регистрации:
  - Username: минимум 2 символа, только буквы латинского алфавита
  - Password: минимум 8 символов, должен содержать буквы и цифры
  - New Password: те же требования, что и для Password

- Реализовать валидацию для новых полей:
  - Full Name: 
    - Два слова, разделенные одним пробелом
    - Только буквы латинского алфавита
    - Каждое слово с большой буквы
    - Пример: "John Doe"
  - Age: 
    - Только целые числа
    - Диапазон от 18 до 100
  - Bio: 
    - От 10 до 200 символов
    - Можно использовать любые символы
  - Email: 
    - Стандартный формат email
    - Пример регулярного выражения: /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/
  - Phone: 
    - Формат: +7XXXXXXXXXX (X - цифры)
    - Пример регулярного выражения: /^\+7\d{10}$/

### 3. Поведение формы
- Валидация должна происходить:
  - При потере фокуса полем (onblur)
  - При отправке формы
- Ошибки должны отображаться:
  - Под каждым полем
  - В том же стиле, что и в форме регистрации
- При успешной валидации:
  - Показать сообщение об успехе
  - Очистить форму

### 4. Интеграция
- В `App.svelte` добавить:
  - Переключение между формами (табы или кнопки)
  - Отображение текущей формы
  - Общий заголовок для форм

### 5. Стилизация
- Использовать существующие стили из RegisterForm
- Сохранить единый стиль отображения ошибок
- Добавить отступы между новыми полями (как в RegisterForm)

## Задача со звёздочкой 🌟
Подумайте над следующими вопросами:
1. Заметили ли вы дублирование кода валидации между формами?
2. Как можно переиспользовать логику валидации для разных типов полей?
3. Какие проблемы могут возникнуть при необходимости изменить правила валидации?
4. Как бы вы организовали валидацию, чтобы легко добавлять новые правила и типы полей?

## Ожидаемый результат
- Две работающие формы с корректной валидацией всех полей
- Понимание проблемы дублирования кода
- Идеи по улучшению архитектуры приложения
- Продуманная структура валидации разных типов полей

## Подсказки
1. Начните с простого копирования базовой логики из RegisterForm
2. Обратите внимание на повторяющийся код валидации
3. Подумайте, как сгруппировать похожие правила валидации
4. Рассмотрите создание переиспользуемых функций валидации для разных типов полей
5. Подумайте, как бы вы организовали код, если бы форм было десять, а типов полей - двадцать?

## Критерии оценки
- Работоспособность обеих форм
- Единообразие валидации
- Качество кода и организация компонентов
- Корректная обработка всех случаев валидации
- Пользовательский опыт (UX):
  - Понятные сообщения об ошибках
  - Логичное поведение форм
  - Удобная навигация между формами

## Дополнительные материалы
- [Документация Svelte по переиспользованию кода](https://svelte.dev/docs#run-time-svelte-store)
- [Паттерны проектирования JavaScript](https://www.patterns.dev/)
- [Принцип DRY (Don't Repeat Yourself)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## Как тестировать
1. Проверить валидацию каждого поля:
   - Ввести некорректные данные
   - Ввести пограничные значения
   - Ввести корректные данные
2. Проверить поведение формы:
   - Заполнить все поля некорректно и попробовать отправить
   - Заполнить все поля корректно и отправить
   - Проверить очистку формы после успешной отправки
3. Проверить навигацию:
   - Переключение между формами
   - Сохранение состояния форм при переключении