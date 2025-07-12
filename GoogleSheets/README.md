# Google Sheets Utilities

A collection of custom Google Sheets functions and utilities to enhance your spreadsheet workflows.

## 📊 Income Tax Calculator

### Overview

The `=IncomeTax(income)` function calculates Australian Income Tax based on the 2025 ATO tax table. This custom function can be used directly in Google Sheets formulas.

![Income Tax Function Example](./Apps%20Script%20Example%20-%20IncomeTax.png)

### Tax Rates (2025 ATO)

| Income Range | Tax Rate | Base Amount |
|--------------|----------|-------------|
| \$0 - \$18,200 | 0% | \$0 |
| \$18,201 - \$45,000 | 16% | \$0 |
| \$45,001 - \$135,000 | 30% | \$4,288 |
| \$135,001 - \$190,000 | 37% | \$31,288 |
| \$190,001+ | 45% | \$51,638 |

### Function Syntax

```javascript
=IncomeTax(income)
```

**Parameters:**
- `income` (number): Annual taxable income in Australian dollars

**Returns:**
- Tax liability amount in Australian dollars

### Examples

| Income | Formula | Result |
|--------|---------|--------|
| \$15,000 | `=IncomeTax(15000)` | \$0 |
| \$30,000 | `=IncomeTax(30000)` | \$1,888 |
| \$80,000 | `=IncomeTax(80000)` | \$14,788 |
| \$150,000 | `=IncomeTax(150000)` | \$36,888 |

## 🛠️ Installation

### Step-by-Step Setup

1. **Open Google Sheets**
   - Open an existing Google Sheet or create a new one

2. **Access Apps Script**
   - Go to **Extensions** → **Apps Script**

3. **Replace Code**
   - Open the `Code.gs` tab (if not already opened)
   - Replace the entire code with the following:

```javascript
/**
 * Calculate Income Tax based on ATO 2025 tax table
 *
 * @param {number} income - Annual taxable income
 * @return {number} The tax liability
 * @customfunction
 */
function IncomeTax(income) {
  if (income <= 18200) {
    return 0; // No tax for income <= $18,200
  } else if (income <= 45000) {
    return (income - 18200) * 0.16; // 16% for income above $18,200
  } else if (income <= 135000) {
    return 4288 + (income - 45000) * 0.3; // $4,288 + 30% for income above $45,000
  } else if (income <= 190000) {
    return 31288 + (income - 135000) * 0.37; // $31,288 + 37% for income above $135,000
  } else {
    return 51638 + (income - 190000) * 0.45; // $51,638 + 45% for income above $190,000
  }
}
```

4. **Save Project**
   - Enter a project name (e.g., `Income Tax Calculator`)
   - Click the **Save** icon to save the project to Drive

5. **Return to Sheet**
   - Go back to your Google Sheet
   - Optionally refresh the browser tab to include the `=IncomeTax()` function in formula auto-fill

6. **Start Using**
   - Use `=IncomeTax(<cell_reference>)` in any cell
   - Example: `=IncomeTax(A1)` where A1 contains the income amount

## 📁 Example Files

- **Example-IncomeTax.gsheet**: Sample spreadsheet demonstrating the function
- **Apps Script Example - IncomeTax.png**: Screenshot showing the function in action

## 🔧 Customization

### Modifying Tax Rates

To update the function for different tax years or jurisdictions:

1. Update the income thresholds in the `if` statements
2. Modify the tax rates (multipliers)
3. Adjust the base amounts for each tax bracket

### Adding New Functions

You can add additional custom functions to the same Apps Script project:

```javascript
/**
 * Calculate effective tax rate
 * @param {number} income - Annual taxable income
 * @return {number} Effective tax rate as percentage
 * @customfunction
 */
function EffectiveTaxRate(income) {
  const tax = IncomeTax(income);
  return income > 0 ? (tax / income) * 100 : 0;
}
```

## ⚠️ Important Notes

- **Accuracy**: This function uses 2025 ATO tax rates. Verify rates for your specific tax year
- **Currency**: All calculations are in Australian dollars
- **Rounding**: Results are not rounded - apply formatting as needed
- **Updates**: Tax rates may change annually - update the function accordingly

## 🐛 Troubleshooting

### Common Issues

1. **Function not found**
   - Ensure the Apps Script project is saved
   - Refresh the Google Sheets tab
   - Check that the function name matches exactly

2. **Incorrect results**
   - Verify the income value is a number
   - Check that the Apps Script code is correctly copied
   - Ensure no extra spaces or characters in the code

3. **Permission errors**
   - Authorize the Apps Script when prompted
   - Grant necessary permissions for custom functions

## 📚 Additional Resources

- [Google Apps Script Custom Functions](https://developers.google.com/apps-script/guides/sheets/functions)
- [ATO Tax Rates](https://www.ato.gov.au/rates/individual-income-tax-rates/)
- [Google Sheets Formula Reference](https://support.google.com/docs/table/25273)

---

**Disclaimer**: This function is for educational and planning purposes. Always consult with a tax professional for official tax calculations.

