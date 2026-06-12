# 表格创建

这是一个NPOI库中XWPFTable类的定义，用于操作Word文档中的表格。下面我将分类解释这些成员的作用：

## 构造函数

- `XWPFTable(CT_Tbl table, IBody part)`：使用现有的CT_Tbl（底层XML结构）和文档部分初始化表格。
- `XWPFTable(CT_Tbl table, IBody part, int row, int col)`：初始化表格并指定初始行数和列数。

## 属性

### 边框相关

- `InsideHBorderType`、`InsideHBorderSize`、`InsideHBorderSpace`、`InsideHBorderColor`：获取表格内部水平边框的类型、大小、间距和颜色。
- `InsideVBorderType`、`InsideVBorderSize`、`InsideVBorderSpace`、`InsideVBorderColor`：获取表格内部垂直边框的类型、大小、间距和颜色。

### 表格样式和布局

- `RowBandSize`、`ColBandSize`：获取或设置行带和列带的大小（用于交替行/列样式）。
- `CellMarginLeft`、`CellMarginBottom`、`CellMarginRight`、`CellMarginTop`：获取单元格的边距（左、下、右、上）。
- `StyleID`：获取或设置表格样式ID。
- `TableCaption`：获取或设置表格标题。
- `TableDescription`：获取或设置表格描述。
- `TableAlignment`：获取或设置表格对齐方式（左、中、右等）。
- `Width`：获取或设置表格宽度。

### 表格结构

- `Rows`：获取表格行的列表。
- `NumberOfRows`：获取表格的行数。
- `NumberOfColumns`：获取表格的列数（注意：这是基于第一行的列数，因为Word表格可能每行列数不同）。

### 其他

- `ElementType`：获取元素类型（表格）。
- `Body`：获取表格所属的正文部分。
- `Part`：获取表格所在的文档部分。
- `PartType`：获取部分类型。
- `Text`：获取表格的文本内容（所有单元格文本的拼接）。

## 方法

### 行操作

- `AddNewCol()`：添加新列（注意：这个方法可能是在表格网格中添加列定义，实际可能需要在每行中添加单元格）。
- `AddRow(XWPFTableRow row)`：在表格末尾添加一行。
- `AddRow(XWPFTableRow row, int pos)`：在指定位置添加一行，返回是否成功。
- `CreateRow()`：创建新行并添加到表格中。
- `GetRow(int pos)`：获取指定位置的行。
- `GetRow(CT_Row row)`：根据CT_Row对象获取对应的XWPFTableRow。
- `InsertNewTableRow(int pos)`：在指定位置插入新行。
- `RemoveRow(int pos)`：移除指定位置的行。

### 表格属性操作

- `GetCTTbl()`：获取底层的CT_Tbl对象（用于直接操作XML）。
- `GetTrPr()`：获取表格行属性（可能用于设置行级别格式）。
- `RemoveTableAlignment()`：移除表格对齐属性。
- `SetCellMargins(int top, int left, int bottom, int right)`：设置单元格边距。
- `SetColumnWidth(int columnIndex, ulong width)`：设置指定列的宽度。

### 边框设置

- `SetBottomBorder`、`SetLeftBorder`、`SetRightBorder`、`SetTopBorder`：分别设置表格底部、左侧、右侧、顶部边框。
- `SetInsideHBorder`、`SetInsideVBorder`：分别设置内部水平边框和内部垂直边框。

## 枚举

- `XWPFBorderType`：定义边框类型，包括无、单线、粗线、双线、点线、虚线、点划线等。

## 1. CT_TblPr 类表格属性

这个类表示表格属性（Table Properties），继承自CT_TblPrBase（其中可能包含一些基本的表格属性）。

### 属性：

- `tblPrChange`：表示表格属性的变更记录（跟踪更改）。

### 方法：

- `Parse`：从XML节点解析表格属性。
- `AddNewJc`：创建并返回一个表格对齐设置（CT_Jc）对象。
- `AddNewTblLayout`：创建并返回一个表格布局类型（CT_TblLayoutType）对象。
- `AddNewTblPPr`：创建并返回一个表格位置属性（CT_TblPPr）对象。
- `IsSetJc`：检查是否设置了表格对齐。
- `UnsetJc`：取消设置表格对齐。

## 2. CT_Tbl 类表格主体

这个类表示整个表格（Table）。

### 属性：

- `tblGrid`：表格网格，用于定义列宽和列数。
- `tblPr`：表格属性。
- `Items` 和 `Items1`：这两个集合包含了表格中的各种元素，如书签、注释、自定义XML、行等。它们使用选择标识符来区分不同的元素类型。

### 方法：

- `Parse`：从XML节点解析表格。
- `AddNewTblGrid`：创建并返回一个新的表格网格（CT_TblGrid）对象。
- `AddNewTblPr`：创建并返回一个新的表格属性（CT_TblPr）对象。
- `AddNewTr`：创建并返回一个新的表格行（CT_Row）对象。
- `GetTrArray`：获取指定索引的表格行（CT_Row）。
- `GetTrList`：获取表格行的列表。
- `InsertNewTr`：在指定位置插入一个新的表格行。
- `RemoveTr`：移除指定位置的表格行。
- `Set`：设置表格内容（用另一个CT_Tbl对象替换当前内容）。
- `SetTrArray`：设置指定位置的表格行。
- `SizeOfTrArray`：获取表格行的数量。

## 3. CT_TblLayoutType 类表格布局类型

这个类表示表格的布局类型。

### 属性：

- `type`：表格布局类型，枚举值（ST_TblLayoutType），可以是固定布局（fixed）或自动调整（autofit）。
- `typeSpecified`：指示type属性是否被设置（用于XML序列化）。

### 方法：

- `Parse`：从XML节点解析表格布局类型。

