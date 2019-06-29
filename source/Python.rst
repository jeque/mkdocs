Python语言学习笔记
===================

Python基础
------------

1.Python编程入门
~~~~~~~~~~~~~~~~~~

*九九乘法表*
#############

- *编写table9x9.py*

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
		

*斐波那契数列*
###############

- *方法1：编写fibonacci.py*

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
		f = Fibonacci()
		
- *方法2：编写fibs.py*

.. code-block:: python
	:linenos:
	
	#! /usr/bin/env python
	#-*- coding: utf-8 -*-
	__author__ = 'Yan'
	
	import time
	
	def fbis(num):
		result = [0,1]
		for i in range(num-2):
			result.append(result[-2] +result[-1])
		return result
	
	def main():
		result = fbis(10)
		fobj = open('E:\\result.txt', 'w+')
		for i, num in enumerate(result):
			print(u'第%d个数是： %d' % (i,num)
			fobj.write('%d'%num)
			time.sleep(1)
	
	if __name__ = '__main__':
		main()

*概率计算*
###########

- *编写Ballprobability.py*

.. code-block:: python
	:linenos:
	
	#! /usr/bin/env python
	#-*- coding: utf-8 -*-
	__author__ = 'Yan'
	
	import random
	
	classs SelectBall(object):
		'''随机选取10个球中1个球的概率'''
		def __init__(self):
			self.fList = [0,1] #设置初始列表
			self.run()
			
		def run(self):
			while True:
				numStr = raw_input('输入测试的次数:')
				try:
					num = int(numStr)
				except ValueError:
					print(u'要求输入一个整数')
					continue
				else:
					break
			ball = [0, 0, 0 ,0, 0, 0 ,0, 0, 0 ,0]
			for i in xrange(num):
				n = random.randint(1,10)
				ball[n-1] +=1
			for i in xrange(1,11):
				print(u'获取第%d 号球的概率为%f' %(i, ball[n-1]*1.0/num))
				
	if __name__ = '__main__':
		SB = SelectBall()

2.Python变量类型
~~~~~~~~~~~~~~~~~~

3.Python语句
~~~~~~~~~~~~~~~~~

4.Python函数
~~~~~~~~~~~~~~~~~

----------------------------------------------------------------------------------------------------------------------------

主流Python Web框架及实战项目
------------------------------

企业级开发框架-Django
~~~~~~~~~~~~~~~~~~~~~~


高并发处理框架-Tornado
~~~~~~~~~~~~~~~~~~~~~~~


支持快速建站的框架-Flask
~~~~~~~~~~~~~~~~~~~~~~~~~~


底层自定义协议网络框架-Twisted
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- linux系统下增加swap空间
- suse系统账号解锁
- awk 指定分隔符，读取csv格式的某些列

实战项目
~~~~~~~~~~
实战1：用Django+PostgreSQL开发移动Twitter
###########################################

实战2：用Tornado+jQuery开发WebSocket聊天室
##############################################

实战3：用Flask+Bootstrap+Restful开发学校管理系统
####################################################

实战4：用Twisted+SQLAlchemy+ZeroMQ开发跨平台物联网消息网关
############################################################


---------------------------------------------------------------------------------------------------------------------------------------------

Python 网络爬虫
-----------------

1.爬虫常用模块介绍
~~~~~~~~~~~~~~~~~~~~~~~

2.Scrapy爬虫框架
~~~~~~~~~~~~~~~~~~

3.Beautiful Soup爬虫
~~~~~~~~~~~~~~~~~~~~~

4.Machanize模拟浏览器
~~~~~~~~~~~~~~~~~~~~~~~

5.Selenium模拟浏览器
~~~~~~~~~~~~~~~~~~~~~~~

-------------------------------------------------------------------------------------------------------------------------

Python及R语言大数据分析
-------------------------

-------------------------------------------------------------------------------------------------------------------------

Python数据结构与算法
---------------------

1.基础知识
~~~~~~~~~~~~

2.计数初步
~~~~~~~~~~~~~

3.归纳、递归及归简
~~~~~~~~~~~~~~~~~~~~

4.遍历
~~~~~~~~

5.分解、合并、解决
~~~~~~~~~~~~~~~~~~~~~~~

6.复杂依赖及其记忆体化
~~~~~~~~~~~~~~~~~~~~~~~

7.匹配、切割及流量
~~~~~~~~~~~~~~~~~~~

