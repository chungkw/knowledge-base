# Representing Data in Excel with JS

#### 30 June 2024

Sometimes, it is a product requirement to export a set of data as an Excel spreadsheet for the end user to easily use, even if there is a UI in the app to display the same data.

In JS, it is possible to create an Excel sheet with the library ExcelJS. To create one, use the library.

```js
const ExcelJS = require("exceljs");

const workbook = new ExcelJS.Workbook();
const worksheet = workbook.addWorksheet();
```

The primary axis is the column. As such, columns are keyed to identify them.

```js
worksheet.columns = [
    { header: "Name", key: "name" }
];
```

The header property is what is displayed. The key is what is used to identify the column programmatically.

Rows can be added according to the key of columns or simply as values in consecutive cells in a row. The data will be on a new row at the end of the sheet, in the corresponding column.

```js
let rowData = {
    name: "John",
};

worksheet.addRow(rowData);
```

Another method can be used to create the row at the top of the sheet or above a specified row number.

```js
worksheet.insertRow(1, rowData);
```

To simply add a row of data, ignoring column keys, is to use an array.

```js
worksheet.addRow([1, 2, 3]);
```

To get a column by its key, use this method.

```js
const col = worksheet.getColumn(key);
```

A column, row or cell can be collectively or individually (whichever applicable) styled and formatted.

```js
col.width = 3.5;
col.alignment = { horizontal: "center" };

col.fill = {
    type: 'pattern',
    pattern: 'darkGrid',
    fgColor: { argb: 'ffffcc00' }
};
```

When done, use this method to save to disk.

```js
workbook.xlsx.writeFile(output).catch((err) => console.warn(err));
```
