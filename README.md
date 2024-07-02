# db-table-api
    轻松管理数据库（支持 mysql, postgreSQL, sqlite3, mssql），支持删除，新增，修改，分页查询，条件匹配查询
    
    配合web端，实现数据管理excel报表展示、新增参数实现关联表查询

# 配置
## 配置参数示例
```json
{
  "Debug": true,
  "ListenPort": "8795",
  "Driver": "mysql",
  "DSN": "root:root@tcp(192.167.1.6:3307)/task",
  "TablePrefix": "",
  "FieldNameFormat": "original",
  "DefaultPrimaryKeyName": "id",
  "BooleanFields": {
    "_": [
        ]
  },
  "IgnoreFields": {
    "_": [
      "password"
    ]
  }
}
```
## 参数说明
参数 | 说明
---- | ---
Debug | 是否开启调试模式（可选值为：true, false），默认为 true
ListenPort |  监听的端口，默认为 8795
Driver |  数据库类型（支持 mysql, postgreSQL, sqlite3, mssql）
DSN | 数据源连接设置
TablePrefix | 表前缀
DefaultPrimaryKeyName | 默认主键名称（默认为 id）
FieldNameFormat | 输出字段是否为驼峰格式（可选值为：original[原样输出], camel[驼峰格式]），启用后 created_at 会转换为 CreatedAt 输出，默认值为 original, 原样输出数据库中字段名称
BooleanFields | 需要转换为布尔值输出的字段名称，"_"中表示全局的，如果需要转换单独的某个表，则填写 "tablename": ["field1", "field2"] 即可
IgnoreFields | 忽略输出的字段，在此范围内的字段都将屏蔽输出，"_"中表示全局的，如果需要设定单独的某个表，则填写 "tablename": ["field1", "field2"] 即可

# 使用方法
## 开启服务
```shell
./db-table-api
```

## 验证服务是否开启
```url
GET http://127.0.0.1:8795/api/ping
```
服务正常的话，则会返回 "OK" 字符串。
## 数据操作

A. 获取数据列表
```url
GET http://127.0.0.1:8795/api/you-access-table-name?page=1&pageSize=10
```
B. 获取某条数据详情
```url
GET http://127.0.0.1:8795/api/you-access-table-name/PK
```
C. 删除某条记录
```url
DELETE http://127.0.0.1:8795/api/you-access-table-name/PK
```
D. 修改某条记录
```url
PUT http://127.0.0.1:8795/api/you-access-table-name/PK
```
CURL
```curl
POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

username=username1&password=pwd1
```

E. 添加记录
```url
POST http://127.0.0.1:8795/api/you-access-table-name
```
CURL
```curl
POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

username=username1&password=pwd1
```
F. 查看数据表
```curl
GET http://127.0.0.1:8795/api/tables
```

