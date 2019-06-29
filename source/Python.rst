Python语言学习笔记
======================

Python基础
---------------------

**1.Python编程入门**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- *九九乘法表*

编写table9x9.py

.. code-block:: python
	:linenos:
	
	#! /usr/bin/env python
	#-*- coding: utf-8 -*-
	__author__ = 'Yan'
	
	classs PrintTable(object):
		'''打印九九乘法表'''
		def __init__(self):
			print(u'开始打印9X9的乘法表格')
			self.print99()
			
		def print99(self):
			for i in xrange(1,10):
				for j in xrange(1,10):
					print('%dX%d=%2s ' %(j,i,i*j)),
				print('\n')
				
	if __name__ = '__main__':
		pt = PrintTable()
		

- *斐波那契数列*

编写fibonacci.py

.. code-block:: python
	:linenos:
	
	#! /usr/bin/env python
	#-*- coding: utf-8 -*-
	__author__ = 'Yan'
	
	classs Fibonacci(object):
		'''返回一个fibonacci数列'''
		def __init__(self):
			self.fList = [0,1] #设置初始列表
			self.main()
			
		def main(self):
			listLen = raw_input('请输入fibonacci数列的长度(3-50):')
			self.checkLen(listLen)
			while len(self.fList) < int(listLen):
				self.fList.append(self.fList[-1] +slef.fList[-2])
			print('得到的fibonacci数列为:\n %s ' %self.fList)
			
		def checkLen(self,Lenth):   #检查输入的数据是否符合要求
			lenList = map(srt,xrange(3,51))
			if lenth in lenList:
				print(u'输入的长度符合标准，继续运行')
			else:
				print(u'只能输入3-50，太长了没有必要')
				exit()
				
	if __name__ = '__main__':
		pt = Fibonacci()

**2.mysql端口号查看和修改**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Linux系统中限制用户su-权限的方法汇总
- glibc文件网站

**3.mysql数据库备份-xtrabackup**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**4.mysql数据库不能使用group by**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


- linux系统下增加swap空间
- suse系统账号解锁
- awk 指定分隔符，读取csv格式的某些列

爬虫 scrapy
---------------------

**1.oracle数据库的优化**
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**2.查找数据库字符集和exp字符集**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**3.oracle11g plsql调试存储过程卡死的处理技巧**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**4.imp和exp数据导入导出**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**5.扩展表空间及临时表空间**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**5.扩展表空间及临时表空间**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Python大数据分析
---------------------

Python开发Web前端
---------------------

Python数据结构与算法
--------------------------------------------