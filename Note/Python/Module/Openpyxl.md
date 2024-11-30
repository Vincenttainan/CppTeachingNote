# **Python 筆記**  
## openpyxl  

## 一、概述  

openpyxl 就是 Python 操作 Excel 的模組  
支援 讀取、創建、修改、儲存等等的功能  

只要在終端機打上這行指令  
就可以安裝 openpyxl 模組  
```
pip install openpyxl
```

然後在 python 內匯入 openpyxl 模組就可以使用了  
```python
import openpyxl
```

## 二、新建一份 Excel  

先假設你的程式碼放在一個名叫 `folder` 的檔案夾底下  
而且命名為 `example_openpyxl.py`  

```
Desktop
└── folder
    └── example_openpyxl.py
```

### 1. 建立一個新的工作簿  
使用 `openpyxl` 內建的 `Workbook` 建立一個新的工作簿  

```python
workbook = openpyxl.Workbook()
```

### 2. 取得工作表  
讀取第一個工作表  

```python
sheet = workbook.worksheets[0]
```

### 3. 寫入  
設定 `sheet` 工作表內 `A1` 的儲存格為 `this is A1`  

```python
sheet['A1'] = "this is A1"
```

### 4. 儲存檔案  

```python
workbook.save('test.xlsx')
```

#### 完整程式碼  

```python
import openpyxl

workbook = openpyxl.Workbook()
sheet = workbook.worksheets[0]
sheet['A1'] = "this is A1"
workbook.save('test.xlsx')
```

#### 小問題  

再看一次 `folder` 檔案夾裡面的檔案  
會發現裡面的東西依然是只有 `example_openpyxl.py`  
並沒有剛剛儲存的 `test.xlsx`  

再檢查一次檔案結構  
```
Desktop
└── folder
    └── example_openpyxl.py
test.xlsx
```

所以只要把  
```python
workbook.save('test.xlsx')
```
改成  
```python
workbook.save('Desktop/folder/test.xlsx')
```
就可以了  

<img width="370" alt="p0" src="https://github.com/user-attachments/assets/3a036ce8-b6c0-4db3-9113-3870ef7f9ab7">  

```
Desktop
└── folder
    ├── test.xlsx
    └── example_openpyxl.py
```

## 三、讀取 Excel  

跟剛剛的檔案一樣  

```
Desktop
└── folder
    ├── test.xlsx
    └── example_openpyxl.py
```

### 讀取 excel  

其實跟剛剛的做法雷同  
只是把 `openpyxl.Workbook()` 改成 `load_workbook()`  
就可以了

```python
workbook = openpyxl.load_workbook('Desktop/folder/test.xlsx')
```

#### 完整程式碼  

```python
import openpyxl

workbook = openpyxl.load_workbook('Desktop/folder/test.xlsx')
sheet = workbook.worksheets[0]
sheet['A2'] = 'this is A2'
workbook.save('Desktop/folder/test.xlsx')
```

<img width="370" alt="p1" src="https://github.com/user-attachments/assets/0c1ec04e-1759-4da5-ac8a-fc10035d6d10">  
