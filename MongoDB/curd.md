## 基本的增删改查

### insert
> 不需要预先创建表，插入数据时表不存在的话会自动创建
> 插入时如果不指定_id,会使用默认的ObjectId
> 插入数据时，数据结构不要求一样
``` sh
db.user.insert({"name":"xiaolizi","password":"123456","age":22})
db.user.insert({"name":"xiaoguizi","password":"123456","age":24,"mobilephone":"13812345678"})
```

### find
> 不带查询条件是默认返回该表所有数据
``` sh
> db.user.find()
{ "_id" : ObjectId("5c14d9c17dfb2e17833c058f"), "name" : "xiaolizi", "password" : "123456", "age" : 22 }
{ "_id" : ObjectId("5c14d9f77dfb2e17833c0590"), "name" : "xiaoguizi", "password" : "123456", "age" : 24, "mobilephone" : "13812345678" }
```
> 带条件查询时返回满足条件的数据

``` sh
> db.user.find({name:"xiaolizi"})
{ "_id" : ObjectId("5c14d9c17dfb2e17833c058f"), "name" : "xiaolizi", "password" : "123456", "age" : 22 }
```

### update 
> 更新除_id外的整条数据为要更新的内容（慎用）
> 使用 $set 方式更新指定字段
> 使用 $unset 删除指定字段
> 要更新的字段在原数据中可以不存在

``` sh
> db.user.update({"name":"xiaolizi"},{"address":"beijing"})
此时已不存在用户名为xiaolizi的数据
> db.user.find({name:"xiaolizi"})
> db.user.find()
{ "_id" : ObjectId("5c14d9c17dfb2e17833c058f"), "address" : "beijing" }
{ "_id" : ObjectId("5c14d9f77dfb2e17833c0590"), "name" : "xiaoguizi", "password" : "123456", "age" : 24, "mobilephone" : "13812345678" }
使用$set更新xiaoguizi的age为30
> db.user.update({"name":"xiaoguizi"},{"$set":{"age":"30"}})
> db.user.find({"name":"xiaoguizi"})
{ "_id" : ObjectId("5c14d9f77dfb2e17833c0590"), "age" : "30", "mobilephone" : "13812345678", "name" : "xiaoguizi", "password" : "123456" }
使用$unset删除age字段
> db.user.update({"name":"xiaoguizi"},{"$unset":{"age":""}})
> db.user.find({"name":"xiaoguizi"})
{ "_id" : ObjectId("5c14d9f77dfb2e17833c0590"), "mobilephone" : "13812345678", "name" : "xiaoguizi", "password" : "123456" }
```

### delete
> remove 命令删除匹配数据
``` sh
> db.user.remove({"name":"xiaoguizi"})
> db.user.remove({_id:ObjectId("5c14d9c17dfb2e17833c058f")})
> db.user.find()
```