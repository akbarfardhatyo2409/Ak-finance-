# AK Finance (Android)

Offline-first personal finance tracker. Kotlin + Jetpack Compose. The selected `.xlsx` file is the primary data store and changes are written immediately after each transaction operation.

## Open in Android Studio
1. Extract this project.
2. Open the `AKFinance` folder in Android Studio (Hedgehog or newer recommended).
3. Use JDK 17 and allow Gradle sync.
4. Run on Android 8.0+ (API 26).

## First run
- Tap **Buat Excel** to create an AK Finance workbook, or use the document icon to open an existing AK Finance `.xlsx` workbook.
- Add transactions with the floating `+` button.
- The app writes changes to the selected file immediately.

## Workbook format
This first implementation owns a simple XLSX format with a `Transactions` sheet and columns: `ID`, `Date`, `Type`, `Category`, `Amount`, `Note`. It intentionally does not rewrite arbitrary third-party Excel workbooks with formulas, macros, formatting, or multiple custom sheets. Use a dedicated AK Finance workbook.

## Current implementation scope
- Dashboard balance, income, expense
- Create/open local `.xlsx` through Android Storage Access Framework
- Add income/expense transactions
- List and delete transactions
- Basic category analytics
- Offline operation; no INTERNET permission or server dependency

## Important engineering notes
- XLSX is a ZIP package containing XML. This project uses Android's built-in ZIP and XML Pull Parser APIs, avoiding an unmaintained Android Apache POI fork.
- The first version rewrites the AK Finance workbook on each save. Keep a separate backup copy for important records. A later hardening pass should add atomic temporary-document writes, workbook schema validation, edit/search/filter, budgets, and automated tests.
- File providers may not support truncating an existing document with `openOutputStream(uri, "wt")` consistently. Test with the target Android document provider; if needed, create a new workbook and replace the selected URI through the Storage Access Framework.
