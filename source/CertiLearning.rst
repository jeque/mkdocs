认证培训学习笔记
==================

AWS架构师认证
---------------

**第一部分：AWS简介，什么是云计算**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 涵盖领域1：设计高可用性、低成本、容错、可扩展的系统

熟悉::

 AWS架构的最佳实践混合IT架构，例如AWS Direct Connect, AWS Storage Gateway, Amazon Virtual Private Cloud[Amazon VPC], AWS Direct Service.
 
 弹性和可伸缩性，例如Auto Scaling, Amazon Simple Queue Service[Amazon SQS], Elastic Load Balancing, Amazon CloudFront
 
- 涵盖领域2：实施/部署

明确::

 确定使用如下服务的技术和方法，包括Amazon Elastic Compute Cloud[Amazon EC2], Amazon Simple Storage Service[Amazon S3], AWS Elastic Beanstalk, AWS CloudFormation, AWS OpsWorks等。
 
 VPC和AWS身份和访问管理（IAM）来编码和实施云解决方案。
 
什么是云计算？
###############

云计算是按需付费定价通过互联网按需交付IT资源和应用程序。

云计算的六大优势
#################

- 变量与资本支出

- 规模经济

- 停止猜测容量

- 提高速度和敏捷性

- 关注业务差异化

- 在几分钟内走向全球

访问AWS平台
#############

要访问AWS云服务，可以使用AWS管理控制台，AWS命令行界面(CLI)或AWS软件开发工具包(SDK)。

计算和网络服务
################

- *Amazon EC2*
 是一项Web服务，可在云中提供可调整大小的计算容量。

- *AWS Lambda*
 是适用于后端Web开发人员的零管理计算平台，可在AWS云上运行代码，并提供精细的定价结构。

- *Auto Scaling*
 允许组织根据为特定工作负载定义的条件自动扩展或缩减Amazon EC2容量。

- *弹性负载均衡*
 Elastic Load Balancing会自动将传入的应用程序流量分布到云中的多个Amazon EC2实例。它可以实现更高水平的容错能力，无缝地提供应用程序流量所需数量的负载平衡容量。

- *AWS Elastic Beanstalk*
 是在AWS上启动并运行Web应用程序的最快速且最简单的方法。开发人员可以简单地上传他们的应用程序代码，并且该服务自动处理所有的细节，例如资源调配、负载平衡、Auto Scaling和监控。它为各种平台提供支持,包括PHP、Java、Python、Ruby、Node.js、.NET和Go。可以全面控制为应用程序提供支持的资源，并可以随时访问底层资源。

- *Amazon VPC*
 虚拟私有云允许组织配置AWS Cloud 的逻辑隔离部分，以便他们可以在虚拟网络中启动AWS资源。通过使用AWS Direct Connect， 企业可以使用硬件或软件虚拟专用网络 (VPN)连接或专用电路将公司数据中心网络扩展到AWS。

- *AWS Direct Connect*
 允许组织建立从其数据中心到AWS的专用网络连接。

- *Amazon Route 53*
 是一种高度可用且可扩展的域名系统(DNS)Web服务。旨在为开发人员和企业提供一种非常可靠且具有成本效益的方式。

存储和内容交付
#################

- *Amazon S3*
 Amazon Simple Storage Service 为开发人员和IT 团队提供高度持久和可扩展的对象存储，可以存储任何数量的任何对象类型。

- *Amazon Glacier*
 是一款安全、耐用且成本极低的存储服务，可用于数据归档和长期备份。
 
- *Amazon ELastic Block Store(Amazon EBS)*
 提供用于Amazon EC2实例的持久块级存储卷。 每个EBS卷都会在其可用区域内自动复制， 以保护组织免受组件故障的影响， 从而提供高性能可用性和耐用性。 通过提供一致的低延迟性能，EBS提供运行各种工作负载所需的磁盘存储。
 
- *AWS Storage Gateway*
 是一种将内部部署软件设备与基于云的存储器相连接的服务，可在组织的本地IT环境与AWS存储基础架构之间提供无缝且安全的集成。
 
- *AWS CloudFront*
 是一项内容交付Web服务。它与其他AWS云服务集成在一起，为开发人员和企业提供了一种轻松的方式，以低延迟、高数据传输速度和最低使用承诺向全球用户分发内容。可用于使用全球边缘位置网络提供整个网站，包括静态、动态、流媒体和交互式内容。
 
数据库服务
##############

- *Amazon关系数据库服务(Amazon RDS)*


- *Amazon DynamoDB*


- *Amazon Redshift*


- *Amazon ElasticCache*



管理工具
###########

- *Amazon CloudWatch*


 


**第二部分：Amazon S3**
~~~~~~~~~~~~~~~~~~~~~~~~~

**第三部分：Amazon EC2和Amazon ELastic Block**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第四部分：Amazon VPC介绍**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第五部分：ELastic Load Balancing，Amazon CloudWatch和Auto Saling**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第六部分：AWS身份和访问管理（IAM）主体**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第七部分：数据库和AWS**
~~~~~~~~~~~~~~~~~~~~~~~~~~

**第八部分：SQS,SWF和SNS**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第九部分：域名系统和Amazon Route 53**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第十部分：Amazon ELasticCache**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第十一部分：AWS上的安全性、风险和合规性及其他关键服务**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**第十二部分：架构最佳实践**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

