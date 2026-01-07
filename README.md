# Docsfox
Document assembly software

Create and fill in templates to create documents

Docsfox - Python plugins for LibreOffice Writer and Notepad++

Bonus feature: Perform multiple Search and Replace operations

[Docsfox Documentation](docs/Docsfox.md)

## What is document assembly software?

Document assembly or document automation software:
- combines information specific to people and organizations
- with one or more pre-defined template documents
- using placeholders or variables and
- alternative phrases and paragraphs
- to create documents tailored to people and organizations.

Document assembly:
- dramatically reduces the time to produce customized documents
- avoids breaching confidial information left in reused documents
- produces consistent, accurate legal documents
- supports making client-specific changes to standard templates

Document assembly applications generally require expensive monthly subscriptions.

## What is special about Docsfox?

Docsfox is an efficient, free, open source document assembly application. 

Docsfox:
- Is free for commercial and personal use
- Has a short learning curve
- Installs on Microsoft Windows
- Works with a range of word processing software
- Is compatible with:
  - MS Word, MS 365, Outlook
  - LibreOffice Writer, Notepad++
  - Google Docs, Gmail and more
- Works with .DOCX, .TXT, .ODT, .HTML, .MD, .CSV and more.

## What risks does Docsfox reduce?

Docsfox avoids the risks of Web-based and AI document generators.

Your confidential client information and proprietary work is:
- Not transferred across the internet
- Not ingested by Big Tech AI and LLMs
- Not stored on third-party servers exposed to the internet
- Under your full control

No need to trust AI or store confidential client information with other companies. Your templates, client data, and documents can remain on your computer or server. If you like, you have the option to use Docsfox with Microsoft 365, Google Docs, and other cloud storage services.

## How Docsfox Works

Docsfox automates document creation through a simple three-step process:

### Step 1: Create a Template

Start with any existing document (contract, letter, form, etc.) and convert it into a reusable template:

1. **Insert Variables** - Replace specific information with placeholders using double angle brackets:
   - Example: `Pat Secada` becomes `<<ClientFirst>> <<ClientLast>>`
   - Variables can be names, addresses, dates, or any custom text
   - Format: `<<VariableName>>`

2. **Add Optional Text** - Mark text that may or may not be included:
   - Example: `<<Option1>>NOT <<Option1/>>` to optionally include the word "NOT"
   - Useful for clauses that apply only in certain situations
   - Format: `<<TagName>>optional text<<TagName/>>`

3. **Save the Template** - Save as .DOCX, .TXT, .ODT, or other supported formats

### Step 2: Create a Data File

Create a CSV spreadsheet with the information to fill into your template:

1. **Column A (VARIABLE)** - The variable name from your template (without << >>)
2. **Column B (TEXT)** - The actual text to insert
3. **Column C (Type)** - Variable type:
   - `V` for standard variables
   - `TF` for optional text (True/False)
   - `R` for search-and-replace operations
4. **Column D (Value)** - For optional text: `T` to include, `F` to exclude
5. **Column E (Description)** - Notes for your reference

You can create one data file per client and reuse it for multiple documents.

### Step 3: Generate the Document

1. **Open your template** in LibreOffice Writer or Notepad++
2. **Run the Docsfox plugin** (Tools menu or macro)
3. **Select your CSV data file** when prompted
4. **Docsfox automatically**:
   - Replaces all variables with your specific text
   - Includes or excludes optional text based on your T/F settings
   - Performs any search-and-replace operations
5. **Review and save** your customized document

### Example Workflow

**Template (Letter FORM.docx):**
```
<<DateOfDocument>>

Dear <<ClientMrMs>> <<ClientLast>>,

<<Option1>>Thank you for your recent inquiry. <<Option1/>>
We are writing regarding <<MatterDescription>>.

<<OptionFileNo>>Our file number: <<OurFileNo>><<OptionFileNo/>>
```

**Data File (Client DATA.csv):**
```
ClientMrMs,Mr.,V,,
ClientLast,Heron,V,,
MatterDescription,Buy-sell agreements for Heron Unlimited,V,,
Option1,,TF,T,Include thank you
OptionFileNo,,TF,T,Include file number
OurFileNo,H-240288,V,,
DateOfDocument,May 30 2025,V,,
```

**Generated Document:**
```
May 30, 2025

Dear Mr. Heron,

Thank you for your recent inquiry.
We are writing regarding Buy-sell agreements for Heron Unlimited.

Our file number: H-240288
```

This process eliminates manual search-and-replace, prevents errors from forgotten placeholders, and saves hours of repetitive work.


# Docsfox
Програмне забезпечення для складання документів

Створення та заповнення шаблонів для створення документів

Docsfox - плагіни Python для LibreOffice Writer та Notepad++

Додаткова функція: Виконання кількох операцій пошуку та заміни

[Документація Docsfox](docs/Docsfox.md)

## Що таке програмне забезпечення для складання документів?

Програмне забезпечення для складання документів або автоматизації документів:
- поєднує інформацію, характерну для людей та організацій
- з одним або кількома попередньо визначеними шаблонами документів
- використовуючи заповнювачі або змінні та
- альтернативні фрази та абзаци
- для створення документів, адаптованих до людей та організацій.

Складання документів:
- значно скорочує час створення індивідуальних документів
- уникає порушення конфіденційної інформації, що залишається у повторно використаних документах
- створює узгоджені, точні юридичні документи
- підтримує внесення змін до стандартних шаблонів, специфічних для клієнта

Програми для складання документів зазвичай вимагають дорогих щомісячних підписок.

## Що особливого в Docsfox?

Docsfox - це ефективна, безкоштовна програма з відкритим кодом для складання документів.

 Docsfox:
- Безкоштовний для комерційного та особистого використання
- Має короткий час навчання
- Встановлюється на Microsoft Windows
- Працює з різноманітним програмним забезпеченням для обробки текстів
- Сумісний з:
- MS Word, MS 365, Outlook
- LibreOffice Writer, Notepad++
- Google Docs, Gmail та іншими
- Працює з .DOCX, .TXT, .ODT, .HTML, .MD, .CSV та іншими.

## Які ризики зменшує Docsfox?

Docsfox уникає ризиків веб-генераторів документів та генераторів документів на основі штучного інтелекту.

Ваша конфіденційна інформація про клієнтів та їхня власна робота:
- Не передається через Інтернет
- Не завантажується штучним інтелектом та LLM від великих технологічних компаній
- Не зберігається на сторонніх серверах, що підключені до Інтернету
- Під вашим повним контролем

Немає потреби довіряти штучному інтелекту або зберігати конфіденційну інформацію про клієнтів в інших компаніях. Ваші шаблони, дані клієнтів та документи можуть залишатися на вашому комп'ютері або сервері.  За бажанням, ви можете використовувати Docsfox з Microsoft 365, Google Docs та іншими хмарними сховищами.

## Як працює Docsfox

Docsfox автоматизує створення документів за допомогою простого процесу з трьох кроків:

### Крок 1: Створення шаблону

Почніть з будь-якого наявного документа (контракт, лист, форма тощо) і перетворіть його на багаторазовий шаблон:

1. **Вставте змінні** - Замініть конкретну інформацію на заповнювачі, використовуючи подвійні кутові дужки:
   - Приклад: `Патрік Секада` стає `<<ClientFirst>> <<ClientLast>>`
   - Змінні можуть бути іменами, адресами, датами або будь-яким іншим текстом
   - Формат: `<<НазваЗмінної>>`

2. **Додайте необов'язковий текст** - Позначте текст, який може бути включений або виключений:
   - Приклад: `<<Опція1>>НЕ <<Опція1/>>` для необов'язкового включення слова "НЕ"
   - Корисно для пунктів, які застосовуються лише в певних ситуаціях
   - Формат: `<<НазваТегу>>необов'язковий текст<<НазваТегу/>>`

3. **Збережіть шаблон** - Збережіть як .DOCX, .TXT, .ODT або інші підтримувані формати

### Крок 2: Створення файлу даних

Створіть електронну таблицю CSV з інформацією для заповнення вашого шаблону:

1. **Стовпець A (VARIABLE)** - Назва змінної з вашого шаблону (без << >>)
2. **Стовпець B (TEXT)** - Фактичний текст для вставки
3. **Стовпець C (Type)** - Тип змінної:
   - `V` для стандартних змінних
   - `TF` для необов'язкового тексту (True/False - Істина/Хибність)
   - `R` для операцій пошуку та заміни
4. **Стовпець D (Value)** - Для необов'язкового тексту: `T` включити, `F` виключити
5. **Стовпець E (Description)** - Примітки для вашої довідки

Ви можете створити один файл даних для кожного клієнта і повторно використовувати його для кількох документів.

### Крок 3: Генерування документа

1. **Відкрийте ваш шаблон** у LibreOffice Writer або Notepad++
2. **Запустіть плагін Docsfox** (меню Інструменти або макрос)
3. **Виберіть ваш CSV файл даних** коли з'явиться запит
4. **Docsfox автоматично**:
   - Замінює всі змінні вашим конкретним текстом
   - Включає або виключає необов'язковий текст на основі ваших налаштувань T/F
   - Виконує будь-які операції пошуку та заміни
5. **Перегляньте і збережіть** ваш індивідуальний документ

### Приклад робочого процесу

**Шаблон (Letter FORM.docx):**
```
<<DateOfDocument>>

Шановний(а) <<ClientMrMs>> <<ClientLast>>,

<<Option1>>Дякуємо за ваш недавній запит. <<Option1/>>
Ми пишемо щодо <<MatterDescription>>.

<<OptionFileNo>>Номер нашої справи: <<OurFileNo>><<OptionFileNo/>>
```

**Файл даних (Client DATA.csv):**
```
ClientMrMs,пан,V,,
ClientLast,Герон,V,,
MatterDescription,Договори купівлі-продажу для Heron Unlimited,V,,
Option1,,TF,T,Включити подяку
OptionFileNo,,TF,T,Включити номер справи
OurFileNo,H-240288,V,,
DateOfDocument,30 травня 2025,V,,
```

**Згенерований документ:**
```
30 травня, 2025

Шановний пан Герон,

Дякуємо за ваш недавній запит.
Ми пишемо щодо Договори купівлі-продажу для Heron Unlimited.

Номер нашої справи: H-240288
```

Цей процес усуває ручний пошук і заміну, запобігає помилкам від забутих заповнювачів і заощаджує години рутинної роботи.