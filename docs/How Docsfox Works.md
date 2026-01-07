# How Docsfox Works

## Overview

Docsfox is a document assembly tool that automates the process of creating customized documents from templates. It uses a simple find-and-replace mechanism combined with optional text handling to transform template documents into personalized documents.

## The Basic Workflow

### 1. Create a Template Document

Start with any document (Word, LibreOffice, or plain text) and insert special markers where you want variable or optional content:

- **Variables**: Use double angle brackets like `<<ClientFirst>>` or `<<ClientLast>>`
- **Optional Text**: Surround text with paired tags like `<<Clause1>>text here<<Clause1/>>`

**Example Template:**
```
Dear <<ClientFirst>> <<ClientLast>>,

Your account with <<ClientOrg>> has been <<Status>>.

<<Clause1>>Please contact us within 30 days.<<Clause1/>>

<<Clause2>>No further action is required.<<Clause2/>>
```

### 2. Create a Data File (CSV)

Create a CSV file (using Excel, LibreOffice Calc, or any spreadsheet program) with your replacement data:

| Find | Replace | Type | Value | Description |
|------|---------|------|-------|-------------|
| ClientFirst | John | | | First name |
| ClientLast | Smith | | | Last name |
| ClientOrg | Acme Corp | | | Organization |
| Status | approved | | | Account status |
| Clause1 | | TF | T | Include contact clause |
| Clause2 | | TF | F | Exclude no-action clause |

**Column Meanings:**
- **Find**: The tag name (without angle brackets)
- **Replace**: The text to insert
- **Type**: Special processing type (V, R, TF)
- **Value**: Action to take (T=include, F=exclude)
- **Description**: Your notes (not used by Docsfox)

### 3. Run Docsfox

**In LibreOffice Writer:**
1. Open your template document
2. Run the Docsfox macro: Tools → Macros → Run Macro → select Docsfox
3. Select your CSV data file
4. Click OK to apply the replacements

**In Notepad++:**
1. Open your template document
2. Run the Docsfox plugin: Plugins → Python Script → Scripts → Docsfox
3. Select your CSV data file
4. The replacements are applied automatically

### 4. Result

Docsfox processes your template and produces:

```
Dear John Smith,

Your account with Acme Corp has been approved.

Please contact us within 30 days.


```

## How the Processing Works

### Step 1: Load the Data File

When you run Docsfox, it:
1. Prompts you to select a CSV file (or uses the last one you selected)
2. Reads the CSV file and creates replacement rules based on the Type and Value columns
3. Remembers your file selection for next time

### Step 2: Process Different Types of Replacements

Docsfox handles three types of replacements:

#### Type 1: Simple Variables (no Type specified)

For rows where the Type column is empty or contains "V":
- Finds `<<TagName>>` in the document
- Replaces it with the value from the Replace column

**Example:**
- CSV: `ClientFirst, John, , ,`
- Finds: `<<ClientFirst>>`
- Replaces with: `John`

#### Type 2: Optional Text (Type = TF)

For rows where Type = "TF":
- Looks for paired tags: `<<TagName>>...<<TagName/>>`
- If Value = "T": Removes only the tags, keeps the text between them
- If Value = "F": Removes everything including the tags and text between them

**Example:**
- CSV: `Clause1, , TF, T,`
- Finds: `<<Clause1>>Please contact us.<<Clause1/>>`
- Replaces with: `Please contact us.`

**Example:**
- CSV: `Clause2, , TF, F,`
- Finds: `<<Clause2>>No action needed.<<Clause2/>>`
- Replaces with: (nothing - all removed)

#### Type 3: Raw Replacement (Type = R)

For rows where Type = "R":
- Finds the exact text in column A (without adding angle brackets)
- Replaces it with the value from column B
- Useful for find-and-replace operations on regular text

### Step 3: Apply Replacements in Order

The processing happens in this order:
1. First, all simple variable replacements (`<<variable>>` → value)
2. Then, raw text replacements (Type = R)
3. Finally, optional text processing (Type = TF)

This order ensures that variables inside optional text are replaced before the optional text tags are removed.

### Step 4: Save Your Document

After Docsfox finishes processing:
- In LibreOffice Writer: Your document is modified and ready to save
- In Notepad++: Your document is modified and ready to save
- Save the document with a new name to preserve your template

## Advanced Features

### Multiple Search and Replace Operations

You can use Docsfox for batch search-and-replace operations by:
- Creating a CSV file with multiple Find/Replace pairs
- Using Type "R" for raw text replacement
- Running Docsfox to apply all replacements at once

### Alternative Clauses

To offer alternative clauses (include one OR the other, but not both):
1. Create two optional text sections with different tags
2. In your CSV, set one to T and the other to F
3. Add a description reminding you they're alternatives

**Example:**
```
Payment is due <<Option1>>upon execution.<<Option1/>><<Option2>>within 30 days.<<Option2/>>
```

CSV:
| Find | Replace | Type | Value | Description |
|------|---------|------|-------|-------------|
| Option1 | | TF | T | Choose Option1 OR Option2 |
| Option2 | | TF | F | Choose Option1 OR Option2 |

### Reusable Client Data Files

Save a separate CSV file for each client, matter, or project:
- `client-acme-corp.csv`
- `client-smith-john.csv`
- `project-website-redesign.csv`

Docsfox remembers your last-used file, making it easy to generate multiple documents for the same client using different templates.

## Technical Implementation

### LibreOffice Version (docsfoxLO.py)

The LibreOffice version uses the LibreOffice UNO API to:
- Access the current document text
- Create search descriptors to find placeholders
- Replace text while preserving formatting
- Handle multi-line optional text blocks

### Notepad++ Version (docsfoxNP.py)

The Notepad++ version uses the Notepad++ Python scripting API to:
- Get and set the entire document text
- Use regular expressions to find and replace text
- Handle multi-line patterns with `[\s\S]*?` regex
- Provide undo/redo support through editor actions

Both versions implement the same logic and support the same CSV format, ensuring consistent results regardless of which editor you use.

## Privacy and Security

### How Docsfox Keeps Your Data Private

1. **All Processing is Local**: Docsfox runs entirely on your computer
2. **No Internet Connection**: The code never sends data over the internet
3. **No Cloud Storage**: Your templates and data stay on your local drive (unless you choose to use cloud storage)
4. **Open Source**: You can review the code to verify there's no data collection
5. **No AI Services**: Unlike online tools, Docsfox doesn't use AI that might train on your data

### What Gets Stored

The only thing Docsfox stores on your computer is:
- The path to your last-used CSV file (in a text file for convenience)
- Nothing else - no templates, no client data, no generated documents

## Comparison to Manual Methods

### Without Docsfox:
1. Open old document
2. Search for "Jane Doe" → Replace with "John Smith"
3. Search for "ABC Company" → Replace with "Acme Corp"
4. Search for each variable individually
5. Manually delete or keep optional clauses
6. Risk leaving old client information in the document
7. Repeat for every document you need to create

### With Docsfox:
1. Open template
2. Run Docsfox
3. Select data file
4. Done - all replacements made correctly

## Tips for Best Results

1. **Use Clear Tag Names**: Use descriptive names like `ClientFirst` instead of `CF`
2. **Add Descriptions**: Use the Description column to document what each tag does
3. **Test Templates**: Create a test CSV with sample data to verify your template
4. **Save Templates Separately**: Keep original templates unchanged; save processed documents with new names
5. **Organize Data Files**: Create a folder structure to organize client/project CSV files
6. **Mind the Spaces**: For optional text, place tags carefully to avoid unwanted spaces
7. **Use Consistent Naming**: Stick to a naming convention across all your templates

---

# Як працює Docsfox

## Огляд

Docsfox - це інструмент для складання документів, який автоматизує процес створення індивідуальних документів із шаблонів. Він використовує простий механізм пошуку та заміни в поєднанні з обробкою додаткового тексту для перетворення шаблонних документів на персоналізовані документи.

## Базовий робочий процес

### 1. Створіть шаблонний документ

Почніть з будь-якого документа (Word, LibreOffice або звичайний текст) і вставте спеціальні маркери там, де ви хочете змінний або додатковий вміст:

- **Змінні**: Використовуйте подвійні кутові дужки, наприклад `<<ІмяКлієнта>>` або `<<ПрізвищеКлієнта>>`
- **Додатковий текст**: Оточіть текст парними тегами, наприклад `<<Пункт1>>текст тут<<Пункт1/>>`

**Приклад шаблону:**
```
Шановний(а) <<ІмяКлієнта>> <<ПрізвищеКлієнта>>,

Ваш обліковий запис у <<ОрганізаціяКлієнта>> було <<Статус>>.

<<Пункт1>>Будь ласка, зв'яжіться з нами протягом 30 днів.<<Пункт1/>>

<<Пункт2>>Подальші дії не потрібні.<<Пункт2/>>
```

### 2. Створіть файл даних (CSV)

Створіть CSV файл (за допомогою Excel, LibreOffice Calc або будь-якої програми для роботи з таблицями) з вашими даними для заміни:

| Знайти | Замінити | Тип | Значення | Опис |
|--------|----------|-----|----------|------|
| ІмяКлієнта | Іван | | | Ім'я |
| ПрізвищеКлієнта | Петренко | | | Прізвище |
| ОрганізаціяКлієнта | Компанія ABC | | | Організація |
| Статус | схвалено | | | Статус облікового запису |
| Пункт1 | | TF | T | Включити пункт про контакт |
| Пункт2 | | TF | F | Виключити пункт про відсутність дій |

**Значення стовпців:**
- **Знайти**: Назва тегу (без кутових дужок)
- **Замінити**: Текст для вставки
- **Тип**: Тип спеціальної обробки (V, R, TF)
- **Значення**: Дія (T=включити, F=виключити)
- **Опис**: Ваші нотатки (не використовується Docsfox)

### 3. Запустіть Docsfox

**У LibreOffice Writer:**
1. Відкрийте шаблонний документ
2. Запустіть макрос Docsfox: Інструменти → Макроси → Виконати макрос → виберіть Docsfox
3. Виберіть ваш CSV файл даних
4. Натисніть OK для застосування замін

**У Notepad++:**
1. Відкрийте шаблонний документ
2. Запустіть плагін Docsfox: Плагіни → Python Script → Скрипти → Docsfox
3. Виберіть ваш CSV файл даних
4. Заміни застосовуються автоматично

### 4. Результат

Docsfox обробляє ваш шаблон і створює:

```
Шановний(а) Іван Петренко,

Ваш обліковий запис у Компанія ABC було схвалено.

Будь ласка, зв'яжіться з нами протягом 30 днів.


```

## Як працює обробка

### Крок 1: Завантаження файлу даних

Коли ви запускаєте Docsfox, він:
1. Пропонує вам вибрати CSV файл (або використовує останній вибраний вами)
2. Читає CSV файл і створює правила заміни на основі стовпців Тип та Значення
3. Запам'ятовує ваш вибір файлу для наступного разу

### Крок 2: Обробка різних типів замін

Docsfox обробляє три типи замін:

#### Тип 1: Прості змінні (Тип не вказано)

Для рядків, де стовпець Тип порожній або містить "V":
- Знаходить `<<НазваТегу>>` у документі
- Замінює його значенням зі стовпця Замінити

**Приклад:**
- CSV: `ІмяКлієнта, Іван, , ,`
- Знаходить: `<<ІмяКлієнта>>`
- Замінює на: `Іван`

#### Тип 2: Додатковий текст (Тип = TF)

Для рядків, де Тип = "TF":
- Шукає парні теги: `<<НазваТегу>>...<<НазваТегу/>>`
- Якщо Значення = "T": Видаляє лише теги, зберігає текст між ними
- Якщо Значення = "F": Видаляє все, включаючи теги та текст між ними

**Приклад:**
- CSV: `Пункт1, , TF, T,`
- Знаходить: `<<Пункт1>>Будь ласка, зв'яжіться з нами.<<Пункт1/>>`
- Замінює на: `Будь ласка, зв'яжіться з нами.`

**Приклад:**
- CSV: `Пункт2, , TF, F,`
- Знаходить: `<<Пункт2>>Дії не потрібні.<<Пункт2/>>`
- Замінює на: (нічого - все видалено)

#### Тип 3: Пряма заміна (Тип = R)

Для рядків, де Тип = "R":
- Знаходить точний текст у стовпці A (без додавання кутових дужок)
- Замінює його значенням зі стовпця B
- Корисно для операцій пошуку та заміни звичайного тексту

### Крок 3: Застосування замін у порядку

Обробка відбувається в такому порядку:
1. Спочатку всі прості заміни змінних (`<<змінна>>` → значення)
2. Потім заміни звичайного тексту (Тип = R)
3. Нарешті, обробка додаткового тексту (Тип = TF)

Цей порядок гарантує, що змінні всередині додаткового тексту замінюються до того, як теги додаткового тексту видаляються.

### Крок 4: Збережіть ваш документ

Після завершення обробки Docsfox:
- У LibreOffice Writer: Ваш документ змінено і готовий до збереження
- У Notepad++: Ваш документ змінено і готовий до збереження
- Збережіть документ під новою назвою, щоб зберегти ваш шаблон

## Розширені функції

### Кілька операцій пошуку та заміни

Ви можете використовувати Docsfox для пакетних операцій пошуку та заміни:
- Створіть CSV файл з кількома парами Знайти/Замінити
- Використовуйте Тип "R" для прямої заміни тексту
- Запустіть Docsfox для застосування всіх замін одночасно

### Альтернативні пункти

Щоб запропонувати альтернативні пункти (включити один АБО інший, але не обидва):
1. Створіть два розділи додаткового тексту з різними тегами
2. У вашому CSV встановіть один на T, а інший на F
3. Додайте опис, який нагадує, що вони альтернативні

**Приклад:**
```
Оплата має бути здійснена <<Варіант1>>після підписання.<<Варіант1/>><<Варіант2>>протягом 30 днів.<<Варіант2/>>
```

CSV:
| Знайти | Замінити | Тип | Значення | Опис |
|--------|----------|-----|----------|------|
| Варіант1 | | TF | T | Виберіть Варіант1 АБО Варіант2 |
| Варіант2 | | TF | F | Виберіть Варіант1 АБО Варіант2 |

### Файли даних клієнтів для повторного використання

Збережіть окремий CSV файл для кожного клієнта, справи або проекту:
- `клієнт-компанія-abc.csv`
- `клієнт-петренко-іван.csv`
- `проект-редизайн-сайту.csv`

Docsfox запам'ятовує ваш останній використаний файл, що полегшує створення кількох документів для того самого клієнта з використанням різних шаблонів.

## Технічна реалізація

### Версія LibreOffice (docsfoxLO.py)

Версія LibreOffice використовує LibreOffice UNO API для:
- Доступу до тексту поточного документа
- Створення дескрипторів пошуку для знаходження заповнювачів
- Заміни тексту зі збереженням форматування
- Обробки багаторядкових блоків додаткового тексту

### Версія Notepad++ (docsfoxNP.py)

Версія Notepad++ використовує Notepad++ Python scripting API для:
- Отримання та встановлення всього тексту документа
- Використання регулярних виразів для пошуку та заміни тексту
- Обробки багаторядкових шаблонів за допомогою регулярного виразу `[\s\S]*?`
- Підтримки скасування/повтору через дії редактора

Обидві версії реалізують однакову логіку та підтримують той самий формат CSV, забезпечуючи послідовні результати незалежно від того, який редактор ви використовуєте.

## Конфіденційність та безпека

### Як Docsfox зберігає ваші дані приватними

1. **Вся обробка є локальною**: Docsfox працює повністю на вашому комп'ютері
2. **Без підключення до Інтернету**: Код ніколи не надсилає дані через Інтернет
3. **Без хмарного сховища**: Ваші шаблони та дані залишаються на вашому локальному диску (якщо ви не вирішите використовувати хмарне сховище)
4. **Відкритий вихідний код**: Ви можете переглянути код, щоб переконатися, що немає збору даних
5. **Без сервісів AI**: На відміну від онлайн-інструментів, Docsfox не використовує AI, який може навчатися на ваших даних

### Що зберігається

Єдине, що Docsfox зберігає на вашому комп'ютері:
- Шлях до вашого останнього використаного CSV файлу (у текстовому файлі для зручності)
- Нічого більше - ні шаблонів, ні даних клієнтів, ні створених документів

## Порівняння з ручними методами

### Без Docsfox:
1. Відкрийте старий документ
2. Знайдіть "Іван Петренко" → Замініть на "Марія Коваленко"
3. Знайдіть "Компанія ABC" → Замініть на "Компанія XYZ"
4. Шукайте кожну змінну окремо
5. Вручну видаляйте або зберігайте додаткові пункти
6. Ризикуєте залишити стару інформацію про клієнта в документі
7. Повторіть для кожного документа, який потрібно створити

### З Docsfox:
1. Відкрийте шаблон
2. Запустіть Docsfox
3. Виберіть файл даних
4. Готово - всі заміни зроблені правильно

## Поради для кращих результатів

1. **Використовуйте зрозумілі назви тегів**: Використовуйте описові назви, такі як `ІмяКлієнта` замість `ІК`
2. **Додайте описи**: Використовуйте стовпець Опис для документування того, що робить кожен тег
3. **Тестуйте шаблони**: Створіть тестовий CSV з зразковими даними для перевірки вашого шаблону
4. **Зберігайте шаблони окремо**: Зберігайте оригінальні шаблони незмінними; зберігайте оброблені документи під новими назвами
5. **Організуйте файли даних**: Створіть структуру папок для організації CSV файлів клієнтів/проектів
6. **Зверніть увагу на пробіли**: Для додаткового тексту розміщуйте теги обережно, щоб уникнути небажаних пробілів
7. **Використовуйте послідовне іменування**: Дотримуйтесь конвенції іменування у всіх ваших шаблонах
