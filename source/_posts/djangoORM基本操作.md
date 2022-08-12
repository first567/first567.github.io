---
layout:
  - page
title: djangoORM基本操作
date: 2022-02-10 16:16:53
tags: 
   - [技术]
   - [django]
---

####  关于ORM基本操作
<!--more-->

然后在项目或app下面的__init__.py文件中指明要用pymysql连接数据库



一、 常用字段和参数
1.1、常用字段
AutoField：
int自增列，必须填入参数 primary_key=True。当models中如果没有自增列，则会自动创建一个列名为id的列。

IntegerField：
一个整数类型,范围在 -2147483648 to 2147483647。(一般不用它来存手机号(位数也不够)，直接用字符串存，)

CharField：
字符类型，必须提供max_length参数， max_length表示字符长度。这个CharField对应mysql中的varchar类型。

DateField：
日期字段，年月日，日期格式  YYYY-MM-DD，相当于Python中的datetime.date()实例。

DateTimeField：
日期时间字段，年月日时分秒，格式 YYYY-MM-DD HH:MM[:ss[.uuuuuu]][TZ]，相当于Python中的datetime.datetime()实例

EmailField：
相当于varchar类型，

DecimalField：
十进制小数。有两个参数：①max_digits，小数总长度  ②decimal_places，有几个小数位

字段合集：
AutoField(Field)
        - int自增列，必须填入参数 primary_key=True

    BigAutoField(AutoField)
        - bigint自增列，必须填入参数 primary_key=True
     
        注：当model中如果没有自增列，则自动会创建一个列名为id的列
        from django.db import models
     
        class UserInfo(models.Model):
            # 自动创建一个列名为id的且为自增的整数列
            username = models.CharField(max_length=32)
     
        class Group(models.Model):
            # 自定义自增列
            nid = models.AutoField(primary_key=True)
            name = models.CharField(max_length=32)
     
    SmallIntegerField(IntegerField):
        - 小整数 -32768 ～ 32767
     
    PositiveSmallIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
        - 正小整数 0 ～ 32767
    IntegerField(Field)
        - 整数列(有符号的) -2147483648 ～ 2147483647
     
    PositiveIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
        - 正整数 0 ～ 2147483647
     
    BigIntegerField(IntegerField):
        - 长整型(有符号的) -9223372036854775808 ～ 9223372036854775807
     
    BooleanField(Field)
        - 布尔值类型
     
    NullBooleanField(Field):
        - 可以为空的布尔值
     
    CharField(Field)
        - 字符类型
        - 必须提供max_length参数， max_length表示字符长度
     
    TextField(Field)
        - 文本类型
     
    EmailField(CharField)：
        - 字符串类型，Django Admin以及ModelForm中提供验证机制
     
    IPAddressField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供验证 IPV4 机制
     
    GenericIPAddressField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供验证 Ipv4和Ipv6
        - 参数：
            protocol，用于指定Ipv4或Ipv6， 'both',"ipv4","ipv6"
            unpack_ipv4， 如果指定为True，则输入::ffff:192.0.2.1时候，可解析为192.0.2.1，开启此功能，需要protocol="both"
     
    URLField(CharField)
        - 字符串类型，Django Admin以及ModelForm中提供验证 URL
     
    SlugField(CharField)
        - 字符串类型，Django Admin以及ModelForm中提供验证支持 字母、数字、下划线、连接符（减号）
     
    CommaSeparatedIntegerField(CharField)
        - 字符串类型，格式必须为逗号分割的数字
     
    UUIDField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供对UUID格式的验证
     
    FilePathField(Field)
        - 字符串，Django Admin以及ModelForm中提供读取文件夹下文件的功能
        - 参数：
                path,                      文件夹路径
                match=None,                正则匹配
                recursive=False,           递归下面的文件夹
                allow_files=True,          允许文件
                allow_folders=False,       允许文件夹
     
    FileField(Field)
        - 字符串，路径保存在数据库，文件上传到指定目录
        - 参数：
            upload_to = ""      上传文件的保存路径
            storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
     
    ImageField(FileField)
        - 字符串，路径保存在数据库，文件上传到指定目录
        - 参数：
            upload_to = ""      上传文件的保存路径
            storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
            width_field=None,   上传图片的高度保存的数据库字段名（字符串）
            height_field=None   上传图片的宽度保存的数据库字段名（字符串）
     
    DateTimeField(DateField)
        - 日期+时间格式 YYYY-MM-DD HH:MM[:ss[.uuuuuu]][TZ]
     
    DateField(DateTimeCheckMixin, Field)
        - 日期格式      YYYY-MM-DD
     
    TimeField(DateTimeCheckMixin, Field)
        - 时间格式      HH:MM[:ss[.uuuuuu]]
     
    DurationField(Field)
        - 长整数，时间间隔，数据库中按照bigint存储，ORM中获取的值为datetime.timedelta类型
     
    FloatField(Field)
        - 浮点型
     
    DecimalField(Field)
        - 10进制小数
        - 参数：
            max_digits，小数总长度
            decimal_places，小数位长度
     
    BinaryField(Field)
        - 二进制类型

mysql与orm字段对应关系
'''
对应关系：
    'AutoField': 'integer AUTO_INCREMENT',
    'BigAutoField': 'bigint AUTO_INCREMENT',
    'BinaryField': 'longblob',
    'BooleanField': 'bool',
    'CharField': 'varchar(%(max_length)s)',
    'CommaSeparatedIntegerField': 'varchar(%(max_length)s)',
    'DateField': 'date',
    'DateTimeField': 'datetime',
    'DecimalField': 'numeric(%(max_digits)s, %(decimal_places)s)',
    'DurationField': 'bigint',
    'FileField': 'varchar(%(max_length)s)',
    'FilePathField': 'varchar(%(max_length)s)',
    'FloatField': 'double precision',
    'IntegerField': 'integer',
    'BigIntegerField': 'bigint',
    'IPAddressField': 'char(15)',
    'GenericIPAddressField': 'char(39)',
    'NullBooleanField': 'bool',
    'OneToOneField': 'integer',
    'PositiveIntegerField': 'integer UNSIGNED',
    'PositiveSmallIntegerField': 'smallint UNSIGNED',
    'SlugField': 'varchar(%(max_length)s)',
    'SmallIntegerField': 'smallint',
    'TextField': 'longtext',
    'TimeField': 'time',
    'UUIDField': 'char(32)',
'''
1.2、字段参数
null：
用于指定某个字段可以为空（null=True）

unique：
如果设置为unique=True 则该字段在此表中必须是唯一的 。

db_index：
如果设置db_index=True，那么该字段会创建索引。

default：
为字段指定默认值

auto_now_add（针对DateTimeField和DateField）：
配置auto_now_add=True，创建数据记录的时候会自动把当前时间添加到数据库，后续的修改该字段不会自动更新。

auto_now（针对DateTimeField和DateField）：
配置上auto_now=True，每次更新数据记录的时候会更新该字段。

1.3、关系字段（外键关联---一对一、一对多、多对多）
ForeignKey：
外键类型在ORM中用来表示外键关联关系，一般把ForeignKey字段设置在 '一对多'中'多'的一方。

ManyToManyField：
外键关联中的多对多关系

OneToOneField：
外键关联中的一对一关系。一对一其实就是把一张数据很多的表按照数据的使用频率分为两张表

关系字段中的参数：
 to：设置要关联的表

to_field：设置要关联的表的字段

on_delete：当删除关联表中的数据时，当前表与其关联的字段的行为。

on_delete=None, #当关联的email数据被删除时候，该数据也会被删除，不存在
on_delete=models.CASCADE, #性质和None一样是默认删除
on_delete=models.DO_NOTHING,   #当关联的数据被删除时，自己不受影响，什么事都不做,不会报错
on_delete=models.PROTECT,   #关联保护，关联的数据不允许被删除，并且触发ProtectError
on_delete=models.SET_NULL, #删除关联数据，自己被设置为null（前提字段需要设置为可空null=True）
db_constraint：是否在数据库中创建外键约束，默认为True。

二、单表查询
在表查询之前，先做一些准备工作。我在tests.py文件中做测试。那么首先要写以下类似于manage.py的代码。

import os

if __name__ == '__main__':
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "day59.settings")
    import django
    django.setup()
    from app01 import models  # 导入要测试的应用的models文件
如果想在测试时，查看内部的sql语句，可以在配置文件中加入一下配置。

LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'console':{
            'level':'DEBUG',
            'class':'logging.StreamHandler',
        },
    },
    'loggers': {
        'django.db.backends': {
            'handlers': ['console'],
            'propagate': True,
            'level':'DEBUG',
        },
    }
}
常用的查询方法：
**********************************查询方法******************************************
	<1> all():                  查询所有结果
	<2> filter(**kwargs):       它包含了与所给筛选条件相匹配的对象
	<3> get(**kwargs):          返回与所给筛选条件相匹配的对象，返回结果有且只有一个，如果符合筛选条件的对象超过一个或者没有都会抛出错误。
	<4> exclude(**kwargs):      它包含了与所给筛选条件不匹配的对象
	<5> order_by(*field):       对查询结果排序('-id')/('price')
	<6> reverse():              对查询结果反向排序 	>>>前面要先有排序才能反向
	<7> count():                返回数据库中匹配查询(QuerySet)的对象数量。
	<8> first():                返回第一条记录
	<9> last():                返回最后一条记录
	<10> exists():              如果QuerySet包含数据，就返回True，否则返回False
	<11> values(*field):        返回一个ValueQuerySet——一个特殊的QuerySet，运行后得到的并不是一系列model的实例化对象，而是一个可迭代的字典序列
	<12> values_list(*field):   它与values()非常相似，它返回的是一个元组序列，values返回的是一个字典序列
	<13> distinct():            从返回结果中剔除重复纪录
返回queryset对象的方法：
all()

filter()

exclude()

order_by()

reverse()

distinct()

values()       返回一个可迭代的字典序列

values_list() 返回一个可迭代的元祖序列
返回具体对象的：
get()

first()

last()
返回布尔值的：
exists()
返回数字的：
count()

2.1、先准备好单表查询操作的表：
class User(models.Model):
    name = models.CharField(max_length=32)
    age = models.IntegerField()
    register_time = models.DateField()
    

    # 为了方便打印查看，定义一下打印的格式
    def __str__(self):
        return '对象的名字%s' % self.name

开始单表操作（测试都写在前面说的__main__方法内部）：
新增数据：
1、基于create新增，通过此方法新增得到的是一个数据对象，可以通过点语法取值

models.User.objects.create(name='shj', age=18, register_time='2019-1-1')
在create的内部，参数也可以是时间类型：

from datetime import datetime
ctime = datetime.now()
models.User.objects.create(name='sr', age=12, register_time=ctime)
2、基于对象的绑定方法新增

user_obj = models.User(name='cr', age=16, register_time='2019-1-2')
user_obj.save()
修改数据：
1、基于对象修改

user_obj = models.User.objects.filter(name='shj').first()
user_obj.age = 20
user_obj.save()
2、基于queryset修改

models.User.objects.filter(name='shj').update(age=18)
删除数据：
1、基于queryset

models.User.objects.filter(name='sr').delete()
2、基于对象

user_obj = models.User.objects.filter(name='cr').first()
user_obj.delete()
查询数据：
1、all()：拿到所有结果

res = models.User.objects.all()
2、filter(**kwargs): 它包含了与所给筛选条件相匹配的对象。filter内可以传多个条件，但要注意这些条件之间是and的关系

res = models.User.objects.filter(name='shj', age=18)
3、get：返回与所给筛选条件相匹配的对象，返回结果有且只有一个，如果符合筛选条件的对象超过一个或者没有都会抛出错误（不推荐使用）

res = models.User.objects.get(name='cr')
4、exclude(**kwargs): 它包含了与所给筛选条件不匹配的对象

res = models.User.objects.exclude(name='shj')
5、order_by(*field): 对查询结果排序，默认是升序。可以在排序的字段前面加一个减号就是降序

res = models.User.objects.order_by('age')
res = models.User.objects.order_by('-age')
6、reverse(): 对查询结果反向排序 >> > 前面要先有排序才能反向

res = models.User.objects.order_by('age').reverse()
7、count(): 返回数据库中匹配查询(QuerySet) 的对象数量。

res = models.User.objects.count()
res = models.User.objects.all().count()
8、first(): 返回第一条记录

res = models.User.objects.all().first()
res = models.User.objects.all()[0]  # 不支持负数的索引取值
9、last(): 返回最后一条记录

res = models.User.objects.all().last()
10、exists(): 如果QuerySet包含数据，就返回True，否则返回False

res = models.User.objects.all().exists()
res = models.User.objects.filter(name='shj', age=3).exists()
11、values(*field): 返回一个ValueQuerySet——一个特殊的QuerySet，运行后得到的并不是一系列 model的实例化对象，而是一个可迭代的字典序列

res = models.User.objects.values('name')  # 列表套字典
res1 = models.User.objects.values('name', 'age')  # 列表套字典

'''
<QuerySet [{'name': 'shj'}, {'name': 'cr'}, {'name': 'zw'}, {'name': 'pj'}]>
<QuerySet [{'name': 'shj', 'age': 18}, {'name': 'cr', 'age': 16}, {'name': 'zw', 'age': 20}, {'name': 'pj', 'age': 20}]>
'''
12、values_list(*field): 它与values()非常相似，它返回的是一个元组序列，values返回的是一个字典序列

res = models.User.objects.values_list('name', 'age')  # 列表套元组

'''
<QuerySet [('shj', 18), ('cr', 16), ('zw', 20), ('pj', 20)]>
'''
13、distinct(): 从返回结果中剔除重复纪录  去重的对象必须是完全相同的数据才能去重

res = models.User.objects.values('name','age').distinct()


 神奇的双下划线查询：
1、大于：__gt

# 查询年纪大于16岁的用户

res = models.User.objects.filter(age__gt=16)
2、小于：__lt

# 查询年纪小于18岁的用户

res = models.User.objects.filter(age__lt=18)
3、大于等于：__gte

# 查询年纪大于等于16岁的用户

res = models.User.objects.filter(age__gte=16)
4、小于等于：__lte

# 查询年纪小于等于16岁的用户

res = models.User.objects.filter(age__lte=16)
5、或：__in

# 查询年龄是16或18或20的用户

res = models.User.objects.filter(age__in=[16,18,20])
6、范围：__range

# 查询年龄在10-16岁之间的用户

res = models.User.objects.filter(age__range=[10,16])
7、年份：__year

# 查询注册是在2019年的用户

res = models.User.objects.filter(register_time__year=2019)
8、包含：__contains

# 查询名字中包含字母r的用户

res = models.User.objects.filter(name__contains='r')
9、包含并忽略大小写：__icontains

# 忽略r大小写

res = models.User.objects.filter(name__icontains='r')
10、以什么开头：__startswith

# 查询名字以s开头的用户

res = models.User.objects.filter(name__startswith='s')
print(res)
11、以什么结尾：__endswith

# 查询名字以j结尾的用户

res = models.User.objects.filter(name__endswith='j')
print(res)


三、多表查询 
表与表之间的关系：
一对一(OneToOneField):一对一字段无论建在哪张关系表里面都可以，但是推荐建在查询频率比较高的那张表里面
一对多(ForeignKey):一对多字段建在多的那一方
多对多(ManyToManyField):多对多字段无论建在哪张关系表里面都可以，但是推荐建在查询频率比较高的那张表里面
正向与反向的概念（跨表查询）：
两个有外键关联的表，表a要拿到表b内的字段，如果表a内有关联表b的外键字段，那么就是正向查询，反之就是反向查询。正向查询按字段，反向查询按表名小写。

正向查找有两种方式：
对象查找：对象.关联字段.字段
字段查找：关联字段__字段
反向查找有两种方式：
对象查找：obj.表名_set，一对一关系的可以不加_set
字段查找：表名__字段
多表查询表分析
一共五张表：author    authordetail    book    publish    book_authors

其中author与authordetail  为一对一的关系，其实一对一可以用ForeignKey来做，但是需要设唯一性约束并且会报警告信息，不建议使用，建议用OneToOneField。用了OneToOneField和用ForeignKey会自动在字段后面加_id
book与author是多对多的关系，用ManyToMany，自动创建关联的表
book与publish是一对多的关系，直接用ForeignKey创建即可
 表的准备：
class Book(models.Model):
    title = models.CharField(max_length=32)
    price = models.DecimalField(max_digits=8, decimal_places=2)
    publish_date = models.DateField(auto_now_add=True)  # 插入数据时自动插入时间
    # 一对多外键
    publish = models.ForeignKey(to='Publish')
    # 多对多外键
    authors = models.ManyToManyField(to='Author')  # 虚拟字段， 信号字段

    def __str__(self):
        return '书籍对象的名字：%s' % self.title

 



class Publish(models.Model):
    name = models.CharField(max_length=32)
    addr = models.CharField(max_length=32)
    email = models.EmailField(max_length=32)

    def __str__(self):
        return '出版社对象的名字：%s' % self.name

 



class Author(models.Model):
    name = models.CharField(max_length=32)
    age = models.IntegerField()
    # 建立到AuthorDetail的一对一的外键
    authordetail = models.OneToOneField(to='AuthorDetail')

    def __str__(self):
        return '作者对象的名字：%s' % self.name

 



class AuthorDetail(models.Model):
    phone = models.CharField(max_length=32)
    addr = models.CharField(max_length=32)
开始操作：
新增数据：
创建一个关联对象，并自动写入数据库，且在第三张双方的关联表中自动新建上双方对应关系。

1、直接写id（出版社表提前插入数据）

models.Book.objects.create(title='红楼梦', price=66.6, publish_id=1)
2、传数据对象

publish_obj = models.Publish.objects.filter(pk=2).first()
models.Book.objects.create(title='西游记',price=99.99,publish=publish_obj)
修改数据：
1、queryset修改

# 直接根据publish_id更改出版社绑定关系

models.Book.objects.filter(pk=2).update(publish_id=3)

# 先获取出版社主键值为2的对象

publish_obj = models.Publish.objects.filter(pk=2).first()

# 再更新

models.Book.objects.filter(pk=2).update(publish=publish_obj)
 2、对象修改

# 先获取到书籍主键值为2的数据对象

book_obj = models.Book.objects.filter(pk=2).first()

# 通过.语法修改属性值

book_obj.publish_id = 3

# 调用save方法保存

book_obj.save()
book_obj = models.Book.objects.filter(pk=2).first()

# 拿到出版社表中主键值为3的对象

publish_obj = models.Publish.objects.filter(pk=3).first()

# 点orm中字段名 传该字段对应的表的数据对象

book_obj.publish = publish_obj
book_obj.save()
删除数据：
1、queryset删除

models.Book.objects.filter(pk=2).delete()
2、对象删除

book_obj = models.Book.objects.filter(pk=3).first()
book_obj.delete()
给书籍绑定与作者之间的关系
添加关系：add，支持传数字或对象，并且都可以传多个

book_obj = models.Book.objects.filter(pk=3).first()

# book表通过authors表做外键关联

book_obj.authors.add(2)  # 传一个
book_obj.authors.add(1,3)  # 传多个
book_obj = models.Book.objects.filter(pk=3).first()
author_obj = models.Author.objects.filter(pk=1).first()
book_obj.authors.add(author_obj)  # 可以传一个对象，同样也可以传多个对象
修改书籍与作者的关系：  set()，  set传的必须是可迭代对象！！！

book_obj = models.Book.objects.filter(pk=7).first()

# 可以传数字和对象，并且支持传多个

book_obj.authors.set((1,))
book_obj.authors.set((1,2,3))
author_list = models.Author.objects.all()
book_obj = models.Book.objects.filter(pk=3).first()
book_obj.authors.set(author_list)
删除书籍与作者的绑定关系：remove

book_obj = models.Book.objects.filter(pk=3).first()
book_obj.authors.remove(1)
book_obj.authors.remove(2,3)
book_obj = models.Book.objects.filter(pk=7).first()
author_obj = models.Author.objects.all().first()
book_obj.authors.remove(author_obj)
author_obj1 = models.Author.objects.all()  # 得到queryset对象
book_obj.authors.remove(*author_obj1)  # 需要将queryset打散
清空当前这个表记录对应的绑定关系：clear

book_obj = models.Book.objects.filter(pk=8).first()
book_obj.authors.clear()
基于对象的表查询：
1、正向（从关联字段所在的表到其关联的表）---点的是关联字段

# 查询书籍是三国演义的出版社邮箱

book_obj = models.Book.objects.filter(title='三国演义').first()
print(book_obj.publish.email)  # 直接通过关联字段publish点就行


# 查询书籍是西游记的作者的姓名

book_obj = models.Book.objects.filter(title='西游记').first()
print(book_obj.authors)  # app01.Author.None
print(book_obj.authors.all())  # <QuerySet [<Author: 作者对象的名字：吴承恩>]>


# 查询作者为吴承恩的电话号码

user_obj = models.Author.objects.filter(name='吴承恩').first()
print(user_obj.authordetail.phone)
2、反向（从被关联的表到关联它的表）---点的是表名小写_set.all()，一对一没有all()，直接点表名即可

# 查询出版社是东方出版社出版的书籍 :一对多字段的反向查询,关联表名_set.all()

publish_obj = models.Publish.objects.filter(name='东方出版社').first()
print(publish_obj.book_set)  # app01.Book.None
print(publish_obj.book_set.all())  # <QuerySet [<Book: 书籍对象的名字：水浒传>]>


# 查询作者佚名写过的所有的书：多对多字段的反向查询，关联表名_set.all()

author_obj = models.Author.objects.filter(name='佚名').first()
print(author_obj.book_set.all())  # <QuerySet [<Book: 书籍对象的名字：水浒传>, <Book: 书籍对象的名字：红楼梦>]>


# 查询作者电话号码是110的作者姓名 ：一对一字段的反向查询

authordetail_obj = models.AuthorDetail.objects.filter(phone=110).first()
print(authordetail_obj.author.name)  # 一对一的没有all()方法，直接点即可
基于双下滑线的查询
1、正向：直接在values里以  关联字段开头__属性

# 查询书籍为三国演义的出版社地址

res = models.Book.objects.filter(title='三国演义').values('publish__addr')
print(res)

# 查询书籍为红楼梦的作者的姓名

res = models.Book.objects.filter(title='红楼梦').values('authors__name')
print(res)

# 查询作者施耐庵的家乡

res = models.Author.objects.filter(name='施耐庵').values('authordetail__addr')
print(res)
2、反向：关联字段不在，values里通过   表名小写__属性

# 查询南方出版社出版的书名

res = models.Publish.objects.filter(name='南方出版社').values('book__title')
print(res)

# 查询电话号码为120的作者姓名

res = models.AuthorDetail.objects.filter(phone=120).values('author__name')
print(res)

# 查询作者曹雪芹的写的书的名字

res = models.Author.objects.filter(name='曹雪芹').values('book__title')
print(res)

# 查询书籍为三国演义的作者的电话号码

res = models.Book.objects.filter(title='三国演义').values('authors__ authordetail __ phone')
print(res)
再看一些查询：（可以在filter过滤的时候就    表名__属性  ，这个不用加引号）

# 查询曹雪芹作者的手机号

# 正向

res = models.Author.objects.filter(name='曹雪芹').values('authordetail__phone')

# 反向

res = models.AuthorDetail.objects.filter(author__name='曹雪芹').values('phone')

# 查询出版社为东方出版社的所有图书的名字和价格

# 正向

res = models.Publish.objects.filter(name='东方出版社').values('book__title','book__price')
print(res)

# 反向

res = models.Book.objects.filter(publish__name='东方出版社').values('title','price')
print(res)

# 查询东方出版社出版的价格大于400的书

# 正向

res = models.Publish.objects.filter(name='东方出版社', book__price__gt=400).values('book__title')
print(res)

# 反向

res = models.Book.objects.filter(publish__name='东方出版社',price__gt=400).values('title')
print(res)
聚合查询：
aggregate()是QuerySet 的一个终止子句，它返回一个包含一些键值对的字典。

键的名称是聚合值的标识符，值是计算出来的聚合值。键的名称是按照字段和聚合函数的名称自动生成出来的。

用到的内置函数：

from django.db.models import Avg, Sum, Max, Min, Count
举例：

from django.db.models import Max,Min,Count,Sum,Avg

# 查询主键值为3的书籍的作者个数

res = models.Book.objects.filter(pk=3).aggregate(count_num=Count('authors'))
print(res)

# 查询所有出版社出版的书的平均价格

res = models.Publish.objects.aggregate(avg_price=Avg('book__price'))
print(res)

# 统计东方出版社出版的书籍的个数

res = models.Publish.objects.filter(name='东方出版社').aggregate(count_num=Count('book__id'))
print(res)
 分组查询（annotate）：类似group by

# 分组查询(group_by)   annotate

# 统计每个出版社出版的书的平均价格

res = models.Publish.objects.annotate(avg_price=Avg('book__price')).values('name','avg_price')
print(res)

# 统计每一本书的作者个数

res = models.Book.objects.annotate(count_num=Count('authors')).values('title','count_num')
print(res)

# 统计出每个出版社卖的最便宜的书的价格

res = models.Publish.objects.annotate(min_price=Min('book__price')).values('name','min_price')
print(res)

# 查询每个作者出的书的总价格

res = models.Author.objects.annotate(sum_price=Sum('book__price')).values('name','sum_price')
print(res)
————————————————
版权声明：本文为CSDN博主「BigMasterSun」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_40406241/article/details/91564707