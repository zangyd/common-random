![http://www.opensource.org/licenses/mit-license.php](https://img.shields.io/badge/license-MIT-blue)
![](https://img.shields.io/badge/java-1.8%2B-yellow)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.apifan.common/common-random/badge.svg "Maven Central")](https://search.maven.org/artifact/com.apifan.common/common-random/1.0.0/jar)
# 随机数据生成器
## 概述
简单易用的随机数据生成器。一般用于开发和测试阶段的数据填充、模拟、仿真、演示等场景。可以集成到各种类型的java项目中使用。

## 优点
- 非常轻量级，容易集成，无需过多第三方依赖
- 简单方便，无需编写冗余代码
- 生成的随机数据比较接近真实数据

## 支持的随机数据类型
- 数字(int/long/double)
- 汉字(简体)
- 邮箱地址
- 中文人名(简体)
- 英文人名
- 虚拟身份证号码(中国大陆)
- 虚拟信用卡号码(Visa/Mastercard/JCB/银联/AmericanExpress)
- 手机号码(中国大陆)
- 省份和城市(中国大陆)
- 邮编(中国大陆)
- 联系地址(中国大陆)
- 车牌号(中国大陆，包括新能源车型)
- 域名
- 静态URL
- 日期(特定日期之前/特定日期之后)
- 时间(过去/未来)
- 时间戳
- 强密码
- 网络昵称(登录名)
- IPv4地址
- 端口号
- QQ号码
- 学历
- 高校名称(数据取自教育部网站)
- 公司名称
- 经纬度(中国)
- 中文短句
- User-Agent(PC/Android/iOS)
- 网卡MAC地址
- RGB颜色值
- HEX颜色值

## 如何使用
### Java版本要求
1.8或更高

### 配置依赖
已发布到maven中央仓库。
```xml
<dependency>
    <groupId>com.apifan.common</groupId>
    <artifactId>common-random</artifactId>
    <version>1.0.0</version>
</dependency>
```

### 基础用法
#### 随机数字
```
//生成1个1~101(不含)之间的随机整数
int a = NumberSource.getInstance().randomInt(1, 101);

//生成8个1~101(不含)之间的随机整数
int[] b = NumberSource.getInstance().randomInt(1, 101, 8);

//生成1个10000000000~20000000001(不含)之间的随机长整数
long c = NumberSource.getInstance().randomLong(10000000000L, 20000000001L);

//生成9个10000000000~20000000001(不含)之间的随机长整数
long[] d = NumberSource.getInstance().randomLong(10000000000L, 20000000001L, 9);

//生成1个0.01~0.51(不含)之间的随机整数
double e = NumberSource.getInstance().randomDouble(0.01D, 0.51D);

//生成8个0.01~0.51(不含)之间的随机整数
double[] f = NumberSource.getInstance().randomDouble(0.01D, 0.51D, 8);
```
#### 随机汉字
```
//生成1个随机汉字
String i = OtherSource.getInstance().randomChinese();

//生成4个随机汉字
String j = OtherSource.getInstance().randomChinese(4);
```
#### 随机人名
##### 中文名
```
//生成1个随机中文人名(性别随机)
String k = PersonInfoSource.getInstance().randomChineseName();

//生成1个随机男性中文人名
String k2 = PersonInfoSource.getInstance().randomMaleChineseName();

//生成1个随机女性中文人名
String k3 = PersonInfoSource.getInstance().randomFemaleChineseName();
```
##### 英文名
```
//生成1个随机英文人名
String l = PersonInfoSource.getInstance().randomEnglishName();
```
##### 生成姓名头像
- 该功能可以根据用户姓名快速生成各类网站、app的用户头像
- 背景颜色随机，数据源取自最近十几年来广受欢迎的颜色，详情参见: [Colors of the Year](https://www.w3schools.com/colors/colors_trends.asp)
- 支持使用自定义字体，但是需要使用者自行保证字体版权合法以避免纠纷
```
//姓名
String name = PersonInfoSource.getInstance().randomChineseName();
//头像文件保存路径
String targetPath = "/home/user/picture/" + name + ".png;

//使用默认的Dialog字体
PersonInfoSource.getInstance().generateNamePicture(name, targetPath);

//使用自定义的字体
String font = "/home/user/font/SourceHanSansCN-Normal.ttf";
PersonInfoSource.getInstance().generateNamePicture(name, targetPath, font);
```

#### 随机生成符合规则的虚拟身份证号码
```
//生成1个随机的虚拟身份证号码，地区为广西壮族自治区，男性，出生日期在1990年11月11日至1999年12月12日之间
LocalDate beginDate = LocalDate.of(1990,11,11);
LocalDate endDate = LocalDate.of(1999,12,12); 
String id1 = PersonInfoSource.getInstance().randomMaleIdCard("广西壮族自治区", beginDate, endDate);

//生成1个随机的虚拟身份证号码，地区为河北省，女性，出生日期在2001年1月11日至2008年2月22日之间
LocalDate beginDate2 = LocalDate.of(2001,1,11);
LocalDate endDate2 = LocalDate.of(2008,2,22);
String id2 = PersonInfoSource.getInstance().randomFemaleIdCard("河北省", beginDate2, endDate2);

//生成1个随机的虚拟身份证号码，地区为广西壮族自治区，男性，年龄为18岁
String id3 = PersonInfoSource.getInstance().randomMaleIdCard("广西壮族自治区", 18);

//生成1个随机的虚拟身份证号码，地区为河北省，女性，年龄为19岁
String id4 = PersonInfoSource.getInstance().randomFemaleIdCard("河北省", 19);
```
注意：
- 身份证号码前6位地区码数据取自[民政部网站2019年公开数据](http://www.mca.gov.cn/article/sj/xzqh/2019/)
- 随机生成的身份证号码符合校验规则，但有可能与真实号码相同

#### 随机虚拟信用卡号码
```
//生成1个随机VISA信用卡号码
String cc1 = PersonInfoSource.getInstance().randomCreditCardNo(CreditCardType.Visa);

//生成1个随机MasterCard信用卡号码
String cc2 = PersonInfoSource.getInstance().randomCreditCardNo(CreditCardType.MasterCard);

//生成1个随机American Express信用卡号码
String cc3 = PersonInfoSource.getInstance().randomCreditCardNo(CreditCardType.Amex);

//生成1个随机银联信用卡号码
String cc4 = PersonInfoSource.getInstance().randomCreditCardNo(CreditCardType.UnionPay);

//生成1个随机JCB信用卡号码
String cc5 = PersonInfoSource.getInstance().randomCreditCardNo(CreditCardType.JCB);
```
注意：
- 随机生成的虚拟信用卡号码只是前缀和位数符合规则，并不能通过校验，也无法用于支付，仅供模拟测试/仿真/项目演示等用途

#### 随机中国大陆手机号
```
//生成1个随机中国大陆手机号
String m = PersonInfoSource.getInstance().randomChineseMobile();
```
#### 随机邮箱地址
```
//生成1个随机邮箱地址，后缀随机，邮箱用户名最大长度为10
String n1 = InternetSource.getInstance().randomEmail(10);

//生成1个随机邮箱地址，后缀为163.com，邮箱用户名最大长度为10
String n2 = InternetSource.getInstance().randomEmail(10, "163.com");
```
#### 随机域名
```
//生成1个随机域名，域名最大长度为16
String dm = InternetSource.getInstance().randomDomain(16);
```
#### 随机IPv4地址
```
//生成1个随机公网IPv4地址
String pub = InternetSource.getInstance().randomPublicIpv4();

//生成1个随机私有(内网)IPv4地址
String prv = InternetSource.getInstance().randomPrivateIpv4();
```
#### 随机端口号
```
//生成1个随机端口号
int port = InternetSource.getInstance().randomPort();
```
#### 随机静态URL
```
//生成1个随机静态URL，后缀为jpg
String url = InternetSource.getInstance().randomStaticUrl("jpg");
```
#### 随机日期
```
//生成1个2020年的随机日期，日期格式为yyyy-MM-dd
String d1 = DateTimeSource.getInstance().randomDate(2020, "yyyy-MM-dd");

//生成1个2020年1月2日之后的随机日期，日期格式为yyyy-MM-dd
String d2 = DateTimeSource.getInstance().randomFutureDate(LocalDate.of(2020,1,2), "yyyy-MM-dd");

//生成1个今天(基于系统时间判断)之后的随机日期，日期格式为yyyy-MM-dd
String d3 = DateTimeSource.getInstance().randomFutureDate("yyyy-MM-dd");

//生成1个2020年1月2日之前1年内的随机日期，日期格式为yyyy-MM-dd
String d4 = DateTimeSource.getInstance().randomPastDate(LocalDate.of(2020,1,2), "yyyy-MM-dd");

//生成1个今天(基于系统时间判断)之前1年内的随机日期，日期格式为yyyy-MM-dd
String d5 = DateTimeSource.getInstance().randomPastDate("yyyy-MM-dd");

//生成1个2020年1月2日之前10年内的随机日期，日期格式为yyyy-MM-dd
String dd = DateTimeSource.getInstance().randomPastDate(LocalDate.of(2020,1,2), 3650, "yyyy-MM-dd");

//生成1个2000年1月11日至2010年2月22日范围之间的随机日期，日期格式为yyyy-MM-dd
LocalDate beginDate = LocalDate.of(2000,1,11);
LocalDate endDate = LocalDate.of(2010,2,22);
String d6 = DateTimeSource.getInstance().randomDate(beginDate, endDate, "yyyy-MM-dd");
```
#### 随机时间
```
//生成过去7天范围内的随机时间
LocalDateTime time1 = DateTimeSource.getInstance().randomPastTime(7);

//生成未来7天范围内的随机时间
LocalDateTime time2 = DateTimeSource.getInstance().randomFutureTime(7);

//生成2020年2月14日当天范围内的随机时间
LocalDateTime time3 = DateTimeSource.getInstance().randomTime(2020, 2, 14);

//生成过去100秒范围内的随机时间
LocalDateTime time4 = DateTimeSource.getInstance().randomPastTime(LocalDateTime.now(), 100);

//生成未来100秒范围内的随机时间
LocalDateTime time5 = DateTimeSource.getInstance().randomFutureTime(LocalDateTime.now(), 100);
```
#### 随机时间戳
```
//生成1个当天范围内的随机时间戳
long ts1 = DateTimeSource.getInstance().randomTimestamp(LocalDate.now());

//生成1个2020年3月6日范围内的随机时间戳
long ts2 = DateTimeSource.getInstance().randomTimestamp(LocalDate.of(2020, 3, 6));

//生成1个介于2020年3月6日12:00:00至2020年3月6日12:30:00之间的随机时间戳
LocalDateTime begin = LocalDateTime.of(2020, 3, 6, 12, 0, 0);
LocalDateTime end = LocalDateTime.of(2020, 3, 6, 12, 30, 0);
long ts3 = DateTimeSource.getInstance().randomTimestamp(begin, end);

//生成1个2020年3月6日12:00:00之后180秒内的随机时间戳
LocalDateTime base1 = LocalDateTime.of(2020, 3, 6, 12, 0, 0);
long ts4 = DateTimeSource.getInstance().randomFutureTimestamp(base1, 180);

//生成1个2020年3月7日13:00:00之前120秒内的随机时间戳
LocalDateTime base2 = LocalDateTime.of(2020, 3, 7, 13, 0, 0);
long ts5 = DateTimeSource.getInstance().randomPastTimestamp(base2, 120);
```
#### 随机强密码
```
//生成1个随机强密码，长度为16，无特殊字符
String pwd1 = PersonInfoSource.getInstance().randomStrongPassword(16, false);

//生成1个随机强密码，长度为16，有特殊字符
String pwd2 = PersonInfoSource.getInstance().randomStrongPassword(16, true);
```

#### 随机地址
```
//随机获取省份
String prv = AreaSource.getInstance().randomProvince();

//随机获取城市(省份+城市，以逗号为分隔符)
String city = AreaSource.getInstance().randomCity(",");

//随机获取邮编
String zipCode = AreaSource.getInstance().randomZipCode();

//生成1个随机中国大陆详细地址
String addr = AreaSource.getInstance().randomAddress();
```

#### 随机中国大陆车牌号
```
//生成1个随机中国大陆车牌号(新能源车型)
String n1 = OtherSource.getInstance().randomPlateNumber(true);

//生成1个随机中国大陆车牌号(非新能源车型)
String n2 = OtherSource.getInstance().randomPlateNumber();
```
#### 随机网络昵称
```
//生成1个随机英文网络昵称，最大长度为8个字符
String nickName = PersonInfoSource.getInstance().randomNickName(8);

//生成1个随机汉字网络昵称，最大长度为8个汉字
String nickName2 = PersonInfoSource.getInstance().randomChineseNickName(8);
```
#### 随机QQ号
```
//生成1个随机QQ号
String nickName = PersonInfoSource.getInstance().randomQQAccount();
```
#### 随机学历
```
//随机获取学历
String degree = EducationSource.getInstance().randomDegree();

//随机获取本科高校名称
String college = EducationSource.getInstance().randomCollege();
```
#### 随机公司名称
```
//随机生成1个公司名称，地区前缀为北京
String companyName = OtherSource.getInstance().randomCompanyName("北京");
```
#### 随机经纬度
注意：仅供测试/模拟/仿真/演示，不一定精确。
```
//随机生成1个纬度
double lat = AreaSource.getInstance().randomLatitude();

//随机生成1个经度
double lng = AreaSource.getInstance().randomLongitude();
```
#### 随机中文短句
```
//随机生成1条中文短句
String sentence = OtherSource.getInstance().randomChineseSentence();
```
#### 随机User-Agent
```
//随机生成1个PC User-Agent
String ua1 = InternetSource.getInstance().randomPCUserAgent();

//随机生成1个Android User-Agent
String ua2 = InternetSource.getInstance().randomAndroidUserAgent();

//随机生成1个iOS User-Agent
String ua3 = InternetSource.getInstance().randomIOSUserAgent();
```
#### 随机网卡MAC地址
```
//随机生成1个网卡MAC地址，使用:作为分隔符
String mac = InternetSource.getInstance().randomMacAddress(":");
```
#### 随机颜色值
```
//随机生成1个RGB颜色值
int[] rgb = OtherSource.getInstance().randomRgbColor();

//随机生成1个16进制(HEX)颜色值
String hex = OtherSource.getInstance().randomHexColor();
```

### 注意事项
- 数据均为随机生成，不代表真实数据
- 通过本程序生成的随机数据适用于模拟测试、仿真、项目演示等场景，但可能与真实数据雷同（纯属巧合），因此使用者请严格遵守相关法律法规