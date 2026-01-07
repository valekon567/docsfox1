# Docsfox Documentation
## Free, secure document assembly software

## Summary

Docsfox is a free, secure, open source application used to assemble customized documents.

**Free:** Docsfox is completely free for commercial and personal use.

In contrast, other document assembly services are expensive and bloated. They cost you time with long learning curves and numerous steps to create document templates. They take your money every month with costly subscriptions. 

**Secure:** Docsfox can work entirely on your computer. It is open source, so you can see it has no code that connects to the internet. You can keep your templates and generated documents local. Optionally, you can use Docsfox with online documents, for example, in Microsoft 365 or Google Docs.

In contrast, online document assembly services raise concerns about the privacy of your client information and document content. They host them in the cloud where they are exposed to security breaches at the vendor. AI built into online services presents other privacy risks.

**Easy:** Learning and using Docsfox are quick and easy. Create and reuse templates from existing documents as needed, undeterred by the prospect of grappling with complexity.

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
DateOfDocument,May 30, 2025,V,,
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
## Alternatives
### Search and replace

The most common, free alternative to Docsfox is your word processor's Search and Replace feature. That method of reusing your work product is:
- **Time-consuming**, requiring multiple passes to replace each piece of variable text
- **Tedious**, involving inspection of the context of each word or phrase
- **Error-prone**, leaving behind names and information that doesn't precisely match
- **Duplicative**, requiring repeated manual task for each one of multiple documents
### Open source software

[DocAssemble] is the only alternative, free, open source document assembly application. It is powerful, complex, and very time-consuming to install, configure and use for template creation. It lends itself to large projects in large, typically non-profit organizations.
### Commercial document assembly subscriptions

Docsfox offers a free, simple alternative. It lacks advanced capabilities of commercial services, yet delivers the most used, labor-saving features.
## Features of Docsfox
### Key features
- Free for commercial and personal use
- Open source
- Unlimited templates, documents, users
- Works with any word processor and editor
- Compatible with .DOCX, .TXT, .MD, .HTML, .ODT and more
- Store templates and documents locally or online
- Simple, assisted template creation
- Variables - fill in names, addresses, anything
- Optional clauses
- Enter a client's data once, generate many documents
- Use a spreadsheet (.CSV) for the field names and text to insert
- Save a reusable spreadsheet for each client, matter or project
### Key limitations
- MS Windows only
- Requires installation of free, open source LibreOffice Writer or Notepad++
- No conditional logic
### Variables

Like other document assembly applications, Docsfox automates the creation of documents from templates. It does the searching and replacing for you. You won't inadvertently leave the old, wrong names and variable information in new documents.
### Optional clauses

Docsfox allows you to have optional and alternative clauses. You can easily choose to include or exclude any of the clauses in your template.
### Safe and private

Completely secure and private, Docsfox operates entirely on your computer. Your text and client information can be kept completely private.  Docsfox does not use AI that sends your content across the internet and may expose it to other users of the AI service.

Docsfox coding is fully transparent. Your data and template text stay on your computer

Docsfox saves you time and prevents drafting mistakes so easy to make when reusing existing documents.

- Works with any word processor application on your computer, including:
	- MS Word
	- LiberOffice Writer
	- WordPerfect Office
	- OpenOffice Writer
	- more...
- Works with online word processors, including:
	- Google Docs
	- Microsoft 365
	- OnlyOffice
	- CKEditor

## Getting started
## Support
### Planned:

| Online manual | YES  |
| ------------- | ---- |
| PDF manual    | YES  |
| Videos        | YES  |
| Screenshots   | YES  |
| Cheat sheet   | YES  |
| Forum         | YES  |
| Email support | No   |
| Phone support | No   |
| Support cost  | Zero |

## Roadmap
- Videos
- Screenshots
- Forum
- Prompt for empty variable value
- Automatically create a data file with variables from a template
