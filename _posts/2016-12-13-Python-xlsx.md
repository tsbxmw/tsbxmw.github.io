---
layout: post
title: Python excel 解析方法，读写
categories: Python
description: 笔记
keywords: Python, excel
---

python xml 解析方法 - xlrd - xlwt - xlsxwriter

## 更新 

* add xlsxwriter 使用方法 at 20180208

## 链接

* [Python excel](https://tsbxmw.github.io/2016/12/13/Python-xlsx)

##  内容

### Python 读取excel文件

* [xlrd 下载地址](https://pypi.python.org/pypi/xlrd)

> 安装方法：
 
      解压 xlrd-1.0.0.tar.gz 
      进入解压文件夹xlrd-1.0.0.tar\dist\xlrd-1.0.0\xlrd-1.0.0
      可以看到setup.py
      运行python setup.py install 即可安装

> 读取excel文件

> 导入xlrd

    import xlrd

> 打开excel

    workbook = xlrd.open_workbook("test.xlsx")

> 获取所有的表格

    worksheets = workbook.sheet_names()

> 查找表格

     for worksheet in worksheets:
        if worksheet == "test":
            sheet = workbook.sheet_by_name("test")

> 获取表格的其他方式
    
    sheet = workbook.sheets()[0]
    sheet = workbook.sheet_by_index(0)


> 计算表格内容行数和列数

    num_row = sheet.nrows
    num_col = sheet.ncols

> 打印某一行或列

    print sheet.row_values(1)
    print sheet.col_values(1)

> 获取制定单元格的数据

    sheet.cell_value(row,col)

> 例子

```python

    #!/usr/bin/python
    # -*- coding: UTF-8 -*-
    import xlrd 
    import sys
    reload(sys)
    sys.setdefaultencoding('utf-8') 

    def openxls(src):
        workboot = xlrd.open_workbook(src)
        worksheets = workboot.sheet_names()
        for worksheet in worksheets:
            if worksheet == 'test.xlsx' :
                sheet = workboot.sheet_by_name('test.xlsx')

        #sheet = workboot.sheets()[0]
        #sheet = workboot.sheet_by_index(0)
        nrow = sheet.nrows
        ncol = sheet.ncols
        print nrow
        print ncol
        
        i = -1
        for date_row in sheet.row_values(1) :
            print date_row
            i = i + 1
            for date_col in sheet.col_values(i):
                print date_col

        print sheet.cell_value(10,2)

    if __name__ == '__main__':
        openxls('api.xlsx')
```

### python 写入 XLXS 文件

* [xlsxwriter 地址](http://xlsxwriter.readthedocs.io/#)

> 安装方法 ：

* official ： http://xlsxwriter.readthedocs.io/getting_started.html#getting-started

* locally using : 1, pip install XlsxWriter  or 2, easy_install XlsxWriter 


> 打开要写的文件

    workwbook = xlsxwriter.Workbook(filename)
    workwsheet = workwbook.add_worksheet()

> 写入内容到对应的行列（单元格）

    col = "test"
    rown = 1
    coln = 1
    workwsheet.write(rown, coln, col)

> 记得关闭 workbook， 不然会报 exception

    workwsheet.close()

    

### LINK
* github python 未上传