所有的路由前缀:/admin

#### 用户登录

```json
@route /signIn
@access 公开
@desc 管理员登录接口
@type:JSON
@method:post
request:{
    adminName: string 管理员用户名
   	password: string 管理员密码
}
response:{
    status:true/false,
    token:""
}
```

#### 1 用户管理页面

1.1

```json
@route /getUsersInfo
@access 公开
@desc 用户管理页面拿到每个学生的信息
@type:JSON
@method:get
response:{
    stuId: string 学号
    stuName: string 学生姓名
    stuEmail: string 学生邮箱
    createTime:date 这个账号的创建时间
}
```

1.2批量编辑用户信息界面

```json
@route /updateUsersInfo
@access 公开
@desc 修改用户角色，密码和状态
@type:JSON
@method:post
request:{
    stuId: string 学号
    role: string 角色
    password: string 密码
    status: boolean 用户状态
}
response:{
    status: boolean 信息是否修改成功
}
```

1.3批量删除用户信息

```json
@route /deleteUserInfo
@access 公开
@desc 删除用户
@type:JSON
@method:post
request:{
    stuId: string 学号
}
response:{
    status: boolean 信息是否修改成功
}
```

1.4搜索框-根据学号查询

```json
@route /getInfoByStuId
@access 公开
@desc 根据学号查询
@type:JSON
@method:post
request:{
    stuId: string 学号
}
response:{
    stuId: string 学号
    stuName: string 学生姓名
    stuEmail: string 学生邮箱
    createTime:date 这个账号的创建时间
}
```

1.5搜索框-根据姓名查询

```json
@route /getInfoByStuName
@access 公开
@desc 根据姓名查询
@type:JSON
@method:post
request:{
    stuName: string 姓名
}
response:{
    stuId: string 学号
    stuName: string 学生姓名
    stuEmail: string 学生邮箱
    createTime:date 这个账号的创建时间
}
```

1.6搜索框-时间模糊查询

```json
@route /getInfoByTime
@access 公开
@desc 根据时间查询
@type:JSON
@method:post
request:{
    createTime: date 这个账号的创建时间
}
response:{
    stuId: string 学号
    stuName: string 学生姓名
    stuEmail: string 学生邮箱
    createTime:date 这个账号的创建时间
}
```

1.7拿到单个用户的信息

```json
@route /getUserInfo
@access 公开
@desc 拿到个人信息
@type:JSON
@method:post
request:{
    stuId:string 学号
}
response:{
    id: string 这个文档在第一个插入时生成的时间戳索引
    stuId: string 学号
    stuName: string 姓名
    class: string 班级
    phone: string 电话
    email: string 邮箱
    qq:    string qq号
    wechat: string 微信号
    github: string github账号
    blog: string 博客网址
    role: string 角色
    password: string 密码
    status: bool 状态
}
```

1.8修改单个用户的信息

```json
@route /updateUserInfo
@access 公开
@desc 修改个人信息
@type:JSON
@method:post
request:{
    stuId: string 学号
    stuName: string 姓名
    class: string 班级
    phone: string 电话
    email: string 邮箱
    qq:    string qq号
    wechat: string 微信号
    github: string github账号
    blog: string 博客网址
    role: string 角色
    password: string 密码
    status: bool 状态
}
response:{
    status:bool  个人信息是否修改成功
}
```

1.9创建用户

```
@route /createUser
@access 公开
@desc 创建用户
@type:JSON
@method:post
request:{
	stuId: string 学号
	stuName: string 姓名
	class: string 班级
	password: string 密码
	role: string 角色
}
response:{
	status: bool 用户是否创建成功
}
```

#### 2 勋章管理界面

2.1勋章分类列表

```json
@route /medalClassList
@access 公开
@desc 勋章分类
@type:JSON
@method:get
response:{
    status: bool 状态
    medalClassArray:　Array 勋章分类数组
    medalClassArray:[
        {
        classId: number 分类id
        className: string 分类名
        medalNum: number 勋章数
        classCreateTime: date 创建时间
        status: bool 是否可见
        medal:{
            name:string 勋章名称
            author:string 勋章创建者
            createTime:date 勋章创建时间
            }
        },
		{},
		.......
]
}

```

2.2修改勋章分类状态

```json
@route /updateMedalClassStatus
@access 公开
@desc 勋章分类状态的修改
@type:JSON
@method:post
request:{
    classId: string 分类名
    status: bool 勋章的状态
}
response:{
	status: bool 是否修改成功
}
```

2.3拿到勋章信息

```json
@route /getClassInfo
@access 公开
@desc 拿到勋章的详细信息
@type:JSON
@method:post
request:{
    className:string 分类名称
}
response:{
    id:string 这个勋章分裂在数据库中的索引
    des: string 勋章描述
    status: bool 勋章分类状态
    medalList: Array 勋章集合
    medalList:[
    	{medalName:勋章名称,author:勋章创建人,createTime:勋章创建时间},
		.......
    ]
}
```

2.4修改编辑勋章

```json
@route /updateClassInfo
@access 公开
@desc 修改勋章的详细信息
@type:JSON
@method:post
request:{
    id:string 这个勋章分裂在数据库中的索引
    className: string 勋章分类名
    des: string 勋章描述
    status: bool 勋章分类状态
    medalList: Array 勋章集合
    medalList:[
    	{medalName:勋章名称,author:勋章创建人,createTime:勋章创建时间},
		.......
    ]
}
response:{
    status:bool 是否修改成功
}
```

2.5每个类下所属勋章展示

```json
@route /medalList
@access 公开
@desc 所属勋章展示
@type:JSON
@method:post
requset:{
    classId: string 勋章分类id
}
response:{
    medalId: string 勋章id
    url: string 勋章简图
    name: string 勋章名称
    author:string勋章作者
    createTime: date  勋章创建时间
    
}
```

2.6删除勋章分类

```json
@route /deleteClass
@access 公开
@desc 删除勋章分类
@type:JSON
@method:post
request:{
    className: string 勋章类的id 
}
response:{
    status:bool 是否删除成功
}
```

2.7批量修改勋章状态

```json
@route /updateMedals
@access 公开
@desc 批量修改勋章
@type:JSON
@method:post
request:{
    medalId:Array[string] 由勋章id组成的数组
    medalId:[
    	id1,id2,id3.....	
    ]
    className: string 这个勋章所处的分类名
    status:bool 这个勋章的状态，是否可见
}

```

2.8修改勋章状态

```json
@route /updateMedalStatus
@access 公开
@desc 修改勋章状态
@type:JSON
@method:post
request:{
    medalId: string 勋章的id
    status: bool 这个勋章是不是可见
}
response:{
    status: bool 是否修改成功
}
```

2.9拿到单个勋章信息

```json
@route /getMedalInfo
@access 公开
@desc 修改单个勋章信息
@type:JSON
@method:post
request:{
    medalId: string 勋章的id
}
response:{
    id:string 这个勋章在数据库中的索引
    medalName: string 勋章名称
    des: string 勋章描述
    ann: string 公告
    class: string 勋章所属分类
    status: bool 勋章状态
    url: 勋章图片的url
}
```

2.10编辑修改单个勋章信息

```json
@route /updateMedalInfo
@access 公开
@desc:编辑修改单个勋章信息
@type:JSON
@method:post
request:{
    id:string 这个勋章的数据库索引
    medalName: string 勋章名称
    des: string 勋章描述
    ann: string 公告
    class: string 勋章所属分类
    status: bool 勋章状态
    url: dataformate 勋章图片
}
response:{
    status: bool 是否修改成功
}
```

2.11删除勋章

```json
@route /deleteMedal
@access 公开
@desc:删除勋章
@type:JSON
@method:post
request:{
    medalId: string 勋章id
}
response:{
    status: bool 是否删除成功
}
```

2.12创建勋章

```json
这个接口和编辑勋章的接口相同
```

2.13从其他类中选择勋章

```json
@route /selectMedalsfromOther
@access 公开
@desc:从其他类中选择勋章
@type:JSON
@method:post
request:{
    medalName: Array[string] 勋章名称的数组
    medalName:[
    	name1,name2......
    ]
}
response:Array 用来存储勋章的信息对象的数组
response:[
    {
        id:string 勋章分类id,
        url:string 勋章图片,
        name:string 勋章名称
        author:string 勋章作者
        status:bool 是否可见
        createTime:data 勋章的创建时间
    },
    ......
]
```

#### 获奖管理BY勋章

3.1拿到所有的获奖情况的信息

```json
@route /getAllAwardsByMedal
@access 公开
@desc:拿到所有的获奖情况的信息
@type:JSON
@method:get
response{
    medalId:string 勋章id
    className:string 勋章分类
    medalName:string 勋章名称
    num:number 获奖人数
}
```

3.2搜索框-通过勋章名字搜索

```json
@route /getByMedalName
@access 公开
@desc:拿到获取某个勋章的所有人的信息
@type:JSON
@method:post
request:{
    medalName:string 勋章的名字
}
response{
    medalId:string 勋章id
    className:string 勋章分类
    medalName:string 勋章名称
    num:number 获奖人数
}
```



3.3拿到获取某个勋章的所有人的信息

```json
@route /getMedalAllUser
@access 公开
@desc:拿到获取某个勋章的所有人的信息
@type:JSON
@method:post
request:{
    medalId:string 勋章的id
}
response{
    stuId: string 学号
  	name:string 用户姓名
    medalId:string 勋章id
    medalName:string 勋章名
    time: date 获得勋章的时间
}
```

3.4新增获奖状况

```json
@route /createAwards
@access 公开
@desc:新增获奖状况
@type:JSON
@method:post
request:{
    medalName:勋章名
    name:获奖人
}
response:{
    status:bool 新增获奖状况是否成功
}
```

3.5删除某个人的某个勋章

```json
@route /deleteOnesMedal
@access 公开
@desc:删除某个人的某个奖项
@type:JSON
@method:post
request:{
    stuId:string 学号
}
response:{
    status:bool 是否删除成功
}
```



#### 获奖管理BY用户

4.1拿到所有的

```json
@route /getAllAwardsByUser
@access 公开
@desc:拿到所有的获奖情况的信息
@type:JSON
@method:get
response{
  stuId: string 学号
  name:string 用户姓名
  class:string 用户班级
  num:number 该用户获得的勋章数量
}
```

4.2搜索框-通过学生姓名搜索

```json
@route /getBystuId
@access 公开
@desc:通过姓名拿到所有的获奖情况的信息
@type:JSON
@method:post
request:{
    name:string 用户姓名
}
response{
  	medalId:string 勋章id
    className:string 勋章分类
    medalName:string 勋章名称
    num:number 获奖人数
}
```

4.3拿到这个用户获取的所有勋章

```json
@route /getOnesAllMedal
@access 公开
@desc:拿到这个用户获取的所有勋章
@type:JSON
@method:post
request:{
    stuId:string 学号
}
response[
    {
    stuId: string 学号
  	name:string 用户姓名
    medalId:string 勋章id
    medalName:string 勋章名
    time: date 获得勋章的时间
    },
    {},
    ......
]
```

#### 公告管理

5.1拿到所有公告

```json
@route /getAllAnn
@access 公开
@desc:拿到所有公告
@type:JSON
@method:get
response:[
    {
    title:string 标题
    author:string 作者
    createTime:date 创建时间
    updateTime:date 更新时间
    status:bool 是否可见 
	},
    {},
	......
]
```

5.2批量删除公告

```json
@route /deleteManyAnn
@access 公开
@desc:删除公告
@type:JSON
@method:post
request:{
    titles:Array 公告名的数组
    titles:[name1,name2......]
}
response:{
    status:bool是否成功删除这个公告
}
```

5.2修改某一个公告的状态是否可见

```json
@route /changeStatus
@access 公开
@desc:修改某一个公告的状态是否可见
@type:JSON
@method:post
request:{
    title:公告名
}
response:{
    status:bool状态是否修改成功
}
```

5.3通过标题拿到一个公告的信息

```json
@route /getAnnInfoBytitle
@access 公开
@desc:通过标题拿到一个公告的信息
@type:JSON
@method:post
request:{
    title:公告名
}
response:{
    id:string 这个公告在数据库中的索引
    titlt:string 公告标题
    des:string 公告描述
    status:bool公告状态
}
```



5.4createAnn创建或者修改公告

```json
@route /createAnn
@access 公开
@desc:通过标题拿到一个公告的信息
@type:JSON
@method:post
request:{
    id:这个公告在数据库中的索引，如果在数据库中还没有存储过这个公告，则为空
    titlt:string 公告标题
    des:string 公告描述
    status:bool公告状态
}
response:{
    status:bool 这个公告是否创建或者修改成功
}
```

