# Bulk Letter Generator

A powerful web-based application for generating, formatting, and managing bulk letters with advanced text markup, variable substitution, and PDF export capabilities.

## Features

### 📝 Core Features
- **Variable Management**: Add, edit, and delete variables dynamically with intuitive UI
- **Template System**: Load, save, download, and upload document templates in JSON format
- **Bulk PDF Generation**: Generate multiple PDFs from CSV data and download as ZIP
- **WYSIWYG Preview**: Real-time PDF preview as you edit (with 2-second debounce)
- **Print Support**: Print directly to any printer or PDF printer

### 🎨 Text Formatting & Markup
- **Inline Formatting**:
  - `[b]Bold text[/b]` - Make text bold
  - `[i]Italic text[/i]` - Make text italic
  - `[u]Underlined text[/u]` - Underline text with font-size-proportional line
  - `[large]Large text[/large]` - Increase text size by 1.5x

- **Block-Level Alignment**:
  - `[center]Centered text[/center]` - Center align an entire paragraph
  - `[left]Left aligned text[/left]` - Left align (default)
  - `[right]Right aligned text[/right]` - Right align a paragraph
  - `[justify]Justified text[/justify]` - Justify text to fill the line width

- **Combined Formatting**:
  ```
  [center][b][large]TITLE[/large][/b][/center]
  [center][b]Subtitle[/b][/center]
  [u][$VariableName][/u]
  ```

### 📄 Page Customization
- **Font Selection**: Choose from multiple fonts (Arial, Times New Roman, Calibri, Courier)
- **Font Size**: Adjustable from 8pt to 28pt
- **Page Sizes**: Support for Letter, A4, A3, Legal, and Tabloid formats
- **Margins**: Customize top, right, bottom, and left margins independently (in inches)

### 📊 Variable System
- **Variable Syntax**: Use `[$VariableName]` to insert variable placeholders
- **Dynamic Addition**: Add variables as needed; unused variables are ignored
- **CSV Integration**: Map CSV columns to variables for bulk generation

## Getting Started

### Opening the Application
1. Open `index.html` in a modern web browser (Chrome, Firefox, Edge, Safari)
2. The application loads with a default template and sample variables

### Basic Workflow

#### 1. Setting Up Variables
- **Add Variable**: Click the "+" button to add a new variable row
- **Delete Variable**: Click the "-" button to remove a variable
- **Edit Values**: Type the variable name in the first field, value in the second field

#### 2. Creating Your Document
- **Type Content**: Write in the letter textarea on the left panel
- **Insert Variables**: Use `[$VariableName]` syntax
- **Apply Formatting**: Use markup tags for bold, italic, etc.
- **View Preview**: Real-time PDF preview updates on the right

#### 3. Page Settings
- **Font**: Select from dropdown
- **Font Size**: Adjust slider
- **Page Size**: Choose paper size
- **Margins**: Set top, right, bottom, left margins in inches

#### 4. Template Management
- **Load Template**: Select a template from the dropdown to load predefined layouts
- **Download Current**: Export current settings, variables, and content as JSON template
- **Upload Template**: Import a previously saved JSON template file

#### 5. Bulk PDF Generation
- **Upload CSV**: Click "Upload CSV" and select your data file
- **Map Columns**: CSV columns should correspond to variable names (header row required)
- **Generate**: Click "Generate All PDFs" to create a ZIP with all letters
- **Download**: The browser will download the ZIP file automatically

#### 6. Output
- **Print**: Use the floating "Print" button to print the current preview
- **Download Template**: Save the current letter as a reusable template
- **Bulk Export**: Generate and download multiple PDFs as ZIP

## Markup Guide

### Syntax Rules

#### Variable Substitution
```
[$VariableName]
```
- Replaced with the variable's value
- Case-sensitive: `[$name]` ≠ `[$Name]`
- Variables must exist in the variable list (unused variables won't break the document)

#### Inline Formatting
Apply formatting to individual words or phrases:

```
This is [b]bold text[/b]
This is [i]italic text[/i]
This is [u]underlined text[/u]
This is [large]larger text[/large]
```

**Combinations:**
```
[b][u]Bold and underlined[/u][/b]
[b][i][large]Bold, italic, and large[/large][/i][/b]
```

#### Block-Level Alignment
Wrap entire paragraphs to set alignment:

```
[center]
This entire paragraph will be centered.
[/center]

[right]
This paragraph will be right-aligned.
[/right]

[justify]
This paragraph will be justified, with text spread evenly across the line width.
[/justify]
```

**Important**: Alignment tags must wrap the **entire paragraph**:
- ✅ Correct: `[center]Your entire paragraph here[/center]`
- ❌ Wrong: `Start of sentence [center]centered part[/center] end of sentence`

### Common Examples

#### Professional Letter Header
```
[center][b][large]COMPANY NAME[/large][/b][/center]
[center]Your Address Here[/center]
[center]Phone: 555-1234[/center]
```

#### Highlighted Information
```
[b]Important Date:[/b] [$DueDate]
[b][u]Account Number:[/u][/b] [$AccountNumber]
```

#### Formatted Table-like Content
```
[b]Project Details:[/b]
• Name: [$ProjectName]
• Budget: [b][$BudgetAmount][/b]
• Timeline: [$Timeline]
```

#### Mixed Formatting Signature Block
```
[right]
[$SignerName]
[u][$SignerTitle][/u]
[i][$CompanyName][/i]
[/right]
```

## CSV File Format

### Requirements
- **Header Row**: First row contains variable names
- **Data Rows**: Subsequent rows contain values for each letter
- **Format**: Standard CSV with comma delimiters
- **Quotes**: Use double quotes for cells containing commas or newlines

### Example CSV
```csv
RecipientName,CompanyName,Amount,DueDate
John Smith,Acme Corp,5000.00,2026-06-01
Jane Doe,Tech Solutions,7500.00,2026-06-15
Bob Johnson,Global Industries,3200.00,2026-05-30
```

### Generated Output
For each row in the CSV, the application generates a unique PDF by:
1. Replacing each variable placeholder with the corresponding CSV value
2. Applying all markup formatting
3. Packaging all PDFs into a single ZIP file

## Templates

### Pre-Loaded Templates

#### Professional Letter
- **Font**: Times New Roman, 12pt
- **Size**: Letter (8.5" x 11")
- **Variables**: RecipientName, CompanyName, CompanyAddress, YourName, YourTitle, YourMessage
- **Features**: Centered title, bold sections, underlined emphasis, professional formatting

#### Invoice Template
- **Font**: Arial, 11pt
- **Size**: A4 (210 x 297mm)
- **Variables**: InvoiceNumber, ClientName, Amount, DueDate, YourCompany
- **Features**: Invoice header, bold payment info, underlined invoice number, right-aligned closing

#### Business Proposal
- **Font**: Calibri, 12pt
- **Size**: Letter (8.5" x 11")
- **Variables**: ClientCompany, ProjectScope, Timeline, Budget, YourCompany, ContactPerson
- **Features**: Centered title, large section headers, highlighted budget, multiple formatting styles

### Creating Custom Templates

#### Manual Creation
1. Create a JSON file with the following structure:
```json
{
  "name": "Template Name",
  "settings": {
    "fontSize": "12",
    "fontFace": "arial",
    "pageSize": "letter",
    "margins": {
      "top": 1,
      "right": 1,
      "bottom": 1,
      "left": 1
    }
  },
  "variables": [
    {
      "name": "VariableName1",
      "value": "default value"
    },
    {
      "name": "VariableName2",
      "value": ""
    }
  ],
  "letterContent": "[center][b]Your letter content here[/b][/center]\n\nUse [$VariableName1] for variables."
}
```

2. Upload via the "Upload Template" button

#### Saving Current Work
1. Adjust all settings (font, margins, font size, page size)
2. Add all required variables
3. Write and format your letter content
4. Click "Download Template" to export as JSON
5. Share or store the template file
6. Use "Upload Template" to load it later

## File Structure

```
Bulk Letter Generator/
├── index.html           # Main application interface
├── app.js              # Core application logic (1000+ lines)
├── style.css           # Styling and layout
├── README.md           # This documentation file
├── Templates/          # Template storage folder
│   ├── professional_letter.json
│   ├── invoice.json
│   └── business_proposal.json
```

## Technical Details

### Libraries & Dependencies
- **jsPDF 2.5.1**: PDF generation (client-side, no server required)
- **JSZip**: ZIP file creation for bulk exports
- **Vanilla JavaScript**: No framework dependencies

### Browser Support
- Chrome 90+
- Firefox 88+
- Edge 90+
- Safari 14+

### PDF Rendering Features
- **Text Wrapping**: Automatic word-wrapping with font-size-aware line breaks
- **Font Styling**: Per-token font style (bold, italic, etc.)
- **Underline**: Font-size-proportional line thickness and positioning
- **Alignment**: Left, center, right, and justified text alignment
- **Line Height**: Adaptive line height based on maximum token font size per line
- **Page Breaking**: Automatic page creation when content exceeds page height
- **Multi-page**: Seamless handling of multi-page documents

### Variable Processing Flow
1. **Detection**: Regex pattern `/\[\$\w+\]/g` finds all `[$varname]` placeholders
2. **Substitution**: Each placeholder replaced with corresponding variable value
3. **Rendering**: Formatted text rendered to PDF with all markup applied
4. **Output**: Final PDF generated with all styling preserved

## Tips & Tricks

### Performance
- **Large Bulk Batches**: Generating 1000+ PDFs may take 30-60 seconds depending on content complexity
- **Debounced Preview**: Preview updates on 2-second idle to prevent lag while typing

### Formatting Best Practices
- **Alignment**: Use full-paragraph alignment tags for best results
- **Emphasis**: Combine `[b]` and `[u]` for maximum emphasis: `[b][u]Important[/u][/b]`
- **Headers**: Center with large: `[center][large][b]TITLE[/b][/large][/center]`
- **Variable Spacing**: Include variables with surrounding text on same line to maintain formatting

### CSV Tips
- **Empty Values**: Allowed; will display blank in letter
- **Special Characters**: Wrap cells in quotes if they contain commas or quotes
- **Numbers vs Text**: Leading zeros preserved if quoted: `"0001"` stays `0001`
- **Newlines**: Use `\n` in quoted cells for line breaks within a variable value

### Common Issues

**Variables Not Replacing:**
- Check syntax: Must be `[$name]` not `[name]` or `$name`
- Variable names are case-sensitive: `[$Name]` ≠ `[$name]`

**Alignment Not Working:**
- Ensure alignment tags wrap the **entire paragraph** only
- Cannot mix aligned and non-aligned text in the same paragraph

**Underline Looks Odd:**
- Underline thickness is proportional to font size
- Smaller fonts = thinner underline (by design)
- Cannot increase beyond 1.5pt line width

**PDF Preview Not Updating:**
- Preview refreshes after 2 seconds of inactivity
- Check browser console for errors (F12)

**Bulk Export Issues:**
- Verify CSV header row matches variable names exactly
- Each row generates one PDF; verify your CSV has data rows
- Some antivirus software may block ZIP downloads (disable temporarily)

## Future Enhancements

Potential features for future versions:
- Multi-column layouts
- Image insertion
- Header/footer support
- Table creation
- Color text support
- Background patterns
- Form fields
- Digital signatures
- Cloud template storage

## License

Free to use and modify for personal or commercial purposes.

## Support

For issues or suggestions:
1. Check the "Common Issues" section above
2. Review template examples in the Templates folder
3. Test with simple content before complex markup

---

**Version**: 1.0  
**Last Updated**: May 2026  
**Created with**: HTML5, CSS3, JavaScript, jsPDF, JSZip
