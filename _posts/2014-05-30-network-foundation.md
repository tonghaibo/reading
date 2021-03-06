---
layout: post
title: 计算机网络-概述
categories: 计算机网络
tags: 计算机网络概述
---

##第一章

1. 因特网发展的三个阶段：
	* 单个网络ARPNET向互联网发展，90年关闭
	* 建成了三级结构的因特网，分为主干网、地区网、校园网（或者企业网）
	* 因为三级结构的迅速扩张，逐渐形成了多层次的ISP（Internet Service Provider）结构的因特网
2. ISP是一个很常见的概念，通俗来说，就是网络服务供应商，ISP从管理结构申请到多个IP地址，同时拥有自己建设的通信线路，以及路由器等联网设备，因此任何机构和个人只要向ISP缴纳一定的费用，就可以从ISP获得IP地址，并通过该ISP接入因特网。比如现在的宽带我世界、铁通、长城宽带等等，都是ISP。
3. 至于为什么不让用户或者机构直接向IP管理结构直接购买IP是因为，IP的分配有一点的规则，各个国家都有相应的计划（比如天朝的功夫网），所以IP地址不零售，只批发给经审批过的合法ISP。因此，因特网只有一个，不同国家的用户通过不同的ISP接入到相同的互联网进行通信。
4. 区分两个概念
	* internet：通用名词，泛指由多个计算机网络互联而成的网络
	* Internet： 专用名词，指当前全球最大的、开放的、由众多网络相互连接而成的特定计算机网络，它采用TCP/IP协议族作为通信的规则，其前身为美国的ARPNET
5. 经常碰到的几种信息转换方式：
	* 电路交换：先建立源点和终点的连接，然后整个报文的比特流连续地从源点直达终点，好像在一个管道中传输
	* 报文交换：整个报文先传送到相邻结点，全部存储下来查找转发表，转发到下一个结点
	* 分组交换（路由器的工作原理）：单个分组（整个报文的一部分）传送到相邻结点，存储下来后查找转发表，转发到下一个结点
6. 几个我N次混淆的概念。。。
	* 广域网WAN（Wide Area Network）：作用范围常为几十到几千公里，一般是国家级别的
	* 城域网MAN（Metropolitan Area Network）：作用距离大概5-50公里，城市范围
	* 局域网LAN（Local Area Network）：一般用微型计算机或者工作站通过高速通信线路相连，但地理范围局限在1公里左右
	* 个人区域网PAN（Personnal Area Network）：近似于个人使用无线技术连接起来的网络，一般作用范围在10m左右的样子
7. 又是模模糊糊的网络体系，有个OSI7层模型和什么5层模型，到底是啥玩意，看了这点终于明白了。OSI是国际标准化组织ISO为因特网打造的网络分层模型，但是却失败了，原因有：
	* OSI的专家们缺乏实际经验，他们在完成OSI标准时缺乏商业驱动力
	* OSI的协议实现起来太复杂，而且运行效率很低
	* OSI的制定标准费时太长，大家都用上互联网了，你丫标准才刚出炉，我们用约定好的TCP/IP协议
	* OSI的层次划分不太合理，部分功能在多层中重复出现

	按照一般的概念，网络技术和设备只有符合有关的国际标准才能大范围的获得工程上的应用。但现在情况反过来了，得到最广泛应用的不是国际化标准组织制定的OSI，而是非国际标准的TCP/IP。所以，靠谱的说，**TCP/IP被称为事实上的国际化标准**
8. 综上，现在的标准有3个
	1. OSI的7层模型：应用层、表示层、会话层、运输层、网络层、数据链路层、物理层
	2. TCP/IP的4层模型：应用层、传输层、网际层、网络接口层
	
	从实质上来说，TCP/IP只有最上面的3层，因为最下面的网络接口层并没有什么具体的内容。因此，学习计算机网络通常结合OSI和TCP/IP的优点，采用一种5层协议的体系结构：**应用层、传输层、网络层、数据链路层、物理层**，这样，既简洁又能把原理说清楚：）
9. 所谓的协议啊标准啊，无非想表达一个意思
	* 语法：怎么说
	* 语义：说什么
	* 同步：何时说
10. 先简单介绍一下5层结构各自的作用吧
	1. 应用层：直接为用户的应用进程服务。在因特网中的应用层协议很多，比如支持万维网的HTTP协议，支持电子邮件的SMTP协议，支持文件传输的FTP协议
	2. 运输层：负责向两个主机中进程之间的通信提供服务，主要有两种协议
		* TCP协议：面向连接的，输出传输的单位是报文段，能够提供可靠的交付
		* UDP协议：无连接的，数据传输的单位是用户数据报，不保证提供可靠的交付，只能提供“尽最大努力交付”，多用于疏松的场景，比如网络会议的视频图像传输
	3. 网络层：负责为分组交换网上的不同主机提供通信服务。在发送数据时，网络层把运输层产生的报文段或者用户数据报封装为分组或包进行传送。在TCP/IP协议中，由于网络层使用IP协议，因此分组成为IP数据报，或简称为数据报。网络层的赢一个任务就是**选择合适的路由**，使源主机传输层下来的分组能高效的发送到目的地。
	4. 数据链路层：将网络层交下来的IP数据报组装成帧，在两个相邻结点间的链路上“透明”的传送帧中的数据。每一帧包括数据和必要的控制信息（比如同步信息、地址信息、差错控制等），典型的帧长是几百字节到一千多字节
	5. 物理层：比特流的透明传输。

##第三章

1. 首先由两个概念分清，
	* 链路：从一个结点到相邻结点的**物理线路**，而中间没有任何的交换结点。在进行数据通信时，两个计算机之间的通信路径往往要经过多段这样的链路。可见，链路只是一条路径的组成部分。
	* 数据链路：当在一条线路上传递数据时，不仅仅需要物理链路，还需要一些必须的通信协议，若把**实现这些协议的硬件和软件加到链路上**，就构成了数据链路。
2. 数据链路层的功能很清晰，就是把上层的IP数据报封装成帧，然后发送到物理层进行透明传输。所以，我们可以得到数据链路层的3个问题：
	1. 封装成帧：首尾加上帧定界信息，规定帧的最大长度MTU
	2. 透明传输：就是对于IP数据报的任何数据，都能成功传输。其中包括对帧定界字符的转义
	3. 差错检测：循环冗余检验CRC。说白了就是约定一个标准，发送前后都检车和这个标准是否对应。对应就正确；不对应就抛弃并重传。
