# 浏览器存储及使用
作者:Maybe@Maxleap

伴随着WEB的发现，浏览器的存储方式及技术不断的发生更改，从刚开始的cookie，到localstorage，sessionStorage,再到IndexedDB,再到现在的Web SQL,作为一名合格的前端开发，当然需要对这些技术了如指掌并熟练掌握，本文将比较全面的介绍常见的浏览器存储以及其使用。

##1.Cookie
Cookie是一个用户通过浏览器浏览网站产出的信息的票根，Cookies通常被用来标示一个网站用户的浏览经历，它可能包含这个用户的个人偏好或访问这个网站的一些输入信息。用户可以自己随意操作他们浏览器中的Cookie。
Cookies 可以通过服务端使用 Set-Cookie Http header来设置和修改，当然也可以使用javascript的document.cookie去操作。

###浏览器兼容性
![Cookie兼容性](http://7xs3q2.com1.z0.glb.clouddn.com/cookie_compatibility.png)
[详细请参考](http://caniuse.com/#search=cookie) http://caniuse.com/#search=cookie

### 在浏览器中操作如下：
```
//读取网站下所有的cookie信息，获取的结果是一个以分号;作为分割的一个字符串
var allCookies = document.cookie;
//例如：在百度首页，获取的如下
// "BAIDUID=B32F2BF6BCB66D5559E199F5B1908F4C:FG=1; PSTM=1444711125; BIDUPSID=9DE77BD4B191F421CA54DB11C954067A; ispeed_lsm=0; MCITY=-289%3A; BDSFRCVID=hWtsJeC62Ag8XZc4Nvqo2MixJD2vkWoTH6aoB7vKuwGS_LREoJS6EG0PtvlQpYD-KiV2ogKK0eOTHvvP; H_BDCLCKID_SF=JbADoDD-JCvbfP0kKtr_MJQH-UnLq-vUbT7Z0l8KtqjJbMnL-TOF5R_eD4c0hUTRtjcW-b7mWIQHDp_65xRh5U-9BPvN04RZLbc4KKJxbPQSVtJXQKcvMq5XhUJiB5O-Ban7LtQxfJOKHICRe5-ajxK; BD_CK_SAM=1; locale=zh; BD_HOME=0; H_PS_PSSID=1455_18241_18559_17000_15227_11651; BD_UPN=123253"

//往原来的已经存在的cookie中加入新的cookie
document.cookie ="test=yui";

//当然也可以在后面加上可选择的选项键值对,例如domain，以及其他path，expires
document.cookie="test=yui;domain=.baidu.com"

//删除cookie，就是让这个cookie值得expires过,就是设置这个expires为0
document.cookie="test=yui;domain=.baidu.com;expires=0");
```
###需要注意的地方：
1.通过上面的代码，可以看到document.cookie是个可访问的属性，但是它有内置的setter和getter的function,而不是一个简单的字符串数据,你的get和set都会调用这些原生内置的函数。

2.cookie支持跨域，可以通过在根域名设置cookie，共享多个子域名的数据。

###Cookie的Chrome浏览器实现
[cookie解析](https://code.google.com/p/chromium/codesearch#chromium/src/net/cookies/parsed_cookie.h):  https://code.google.com/p/chromium/codesearch#chromium/src/net/cookies/parsed_cookie.h

##2.Web Storage
Web Storage有两种机制,分别为sessionStorage和localStorage。
sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage是一种半持久化的本地存储（会话级别的存储），而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

这两个对象，对外的方法主要有: setItem,getItem,以键值对的形式存储和读取,key按照索引获取当前存储的key值,找不到时返回null，length属性代表当前存储的key，value对数

###浏览器兼容性
![Web Storage浏览器兼容性](http://7xs3q2.com1.z0.glb.clouddn.com/storage_comoatibility.png)
[详细请参考](http://caniuse.com/#search=localstorage): http://caniuse.com/#search=localstorage
### 代码示例(以localStorage为例)
```
var username = 'helloworld';
var storageUsername;
var randomArr = [Math.random(),Math.random(),Math.random(),Math.random()];
var storageRandomArr;

//storage username,key值区分大小写,存入的内容为这个变量调用toString方法的结果
localStorage.setItem("username",username);

//获取
storageUserName  = localstorage.getItem("username");
//"helloworld"

//删除
localStorage.removeItem("username");

storageUserName  =  localstorage.getItem("username");
// null

//存储对象时，可以先调用JSON.stringify方法，然后取出的时候再调用JSON.parse方法获取结果
localStorage.setItem("randomarr",JSON.stringify(randomArrr));
storageRandomArr = JSON.parse(localStorage.getItem("randomarr"));

Object.prototype.toString.call(storageRandomArr);
// "object Array"

```

##3.IndexDB
IndexedDB 是一个为了能够在客户端存储可观数量的结构化数据，并且在这些数据上使用索引进行高性能检索的 API。

IndexedDB 分别为同步和异步访问提供了单独的 API ,异步 API 方法调用完后会立即返回，而不会阻塞调用线程。

要异步访问数据库，要调用 window 对象 indexedDB 属性的 open() 方法。该方法返回一个 IDBRequest 对象 (IDBOpenDBRequest)；异步操作通过在 IDBRequest 对象上触发事件来和调用程序进行通信。

IndexDb是NoSQL数据库，是一种支持事务的浏览器数据库，基本操作就是，打开数据库，增删改查各种。
###浏览器兼容性
![IndexDB兼容性](http://7xs3q2.com1.z0.glb.clouddn.com/indexdb_compatibility.png)
[详细请参考](http://caniuse.com/#search=IndexDB): http://caniuse.com/#search=IndexDB
###代码示例 - 1.打开数据库
```
//处理浏览器兼容性
window.indexedDB = window.indexedDB || window.webkitIndexedDB || window.mozIndexedDB || window.msIndexedDB;

//如果该数据库MyDatabase不存在，则会被创建；如果已经存在，则被打开。
var request = window.indexedDB.open("MyDatabase");

//打开数据库失败的回调
request.onerror = function(event) {
  console.log("failure");
};
//代开数据成功的回调
request.onsuccess = function(event) {
  console.log("success");
};
```
###代码示例 - 2.初始化数据库
```
var dbName = "MyDatabase";
var dbVersion = 2;//整数
// open函数接受的第二个参数，代表数据的版本，当打开的版本号比当前的版本号大时，会触发onupgradeneeded这个回调
var request = window.indexedDB.open(dbName,dbVersion);
var studentsData = [{
    id:"001",name:"xiaoming",email:0
},{
    id:"002",name:"xiaoxiang",email:1
}];
var tableName = 'students';

request.onerror = function (event) {
    //错误处理
};

request.onupgradeneeded = function (event) {
    var db = event.target.result;
    //创建表,以id字段作为主键来确保唯一，使用keyPath表示
    var objectStore = db.createObjectStore(tableName, { keyPath: "id" });

    //给表添加索引
    objectStore.createIndex("name","name",{unique:false});//非unique索引
    objectStore.createIndex("email","email",{unique:true});//email字段作为unique索引

    for(var i in studentsData){
        //插入数据
        objectStore.add(studentsData[i]);
    }

    console.log("---init db success---");
}
```



###代码示例 - 3.使用事务添加、删除数据
transaction() 方法接受两个参数并返回一个事务对象。第一个参数是事务希望跨越的对象存储空间的列表,即数据库中的表名称。如果你希望事务能够跨越所有的对象存储空间你可以传入一个空数组。第二个参数如果你没有为第二个参数指定任何内容，默认只读。

![事务方法接受参数](http://7xs3q2.com1.z0.glb.clouddn.com/transaction_function.png)

####插入学生003，004，005
```
var dbName = "MyDatabase";
var request = window.indexedDB.open(dbName);
var addData = [{
    id:"003",name:"xiaofang1",email:"3@qq.com"
},{
    id:"004",name:"xiaofang2",email:"4@qq.com"
},{
    id:"005",name:"xiaofang3",email:"5@qq.com"
}];
var tableName = 'students';

//打开数据库失败的回调
request.onerror = function(event) {
    console.log("open indexDb database failure");
};
//代开数据成功的回调
request.onsuccess = function(event) {
    var db = event.target.result;
    var transaction = db.transaction([tableName],'readwrite');
    var objectStore;
    var i;

    //事务主要有三个回调，error，abort，success
    transaction.onerror = function (event) {
        //处理错误
        console.log(event);
    }
    transaction.onbort = function () {
        //事务中断处理
    }
    transaction.oncomplete = function () {
        console.log("添加数据成功");
    }

    objectStore  = transaction.objectStore(tableName);

    for(i  in addData){
        var request = objectStore.add(addData[i]);

        request.onsuccess = function (event) {
            console.log("add one success");
        }
    }
};
```

####删除001学生
```
var dbName = "MyDatabase";
var request = window.indexedDB.open(dbName);
var db;
var tableName = 'students';

request.onerror = function () {
};

request.onsuccess  = function (event) {
    var objectStore;
    var transaction;

    db =  event.target.result;
    transaction= db.transaction([tableName],'readwrite');
    transaction.onerror = function (event) {
        //处理错误
        console.log("error when delete 001 "+ event.target.errorCode);
    }
    transaction.onbort = function () {
        //事务中断处理
    }
    transaction.oncomplete = function () {
        console.log("删除学生001成功");
    }
    objectStore = transaction.objectStore(tableName);
    objectStore.delete("001");
};
```

###代码示例 - 4.使用索引查找数据
主要调用IDBObjectStore示例对象的index方法

```
var dbName = "MyDatabase";
var request = window.indexedDB.open(dbName);
var db;
var tableName = 'students';

request.onerror = function () {
};

request.onsuccess  = function (event) {
    var index;
    var objectStore;

    db =  event.target.result;
    objectStore = db.transaction([tableName]).objectStore(tableName);
    //根据索引字段email朝找3@qq.com的学生
    index = objectStore.index("email").get("3@qq.com");
    index.onsuccess = function(event) {
        console.log(event.target.result);
    };
    index.onerror = function (event) {
        console.log("error when find  by index "+ event.target.errorCode);
    }
};
```

####indexDb还有游标查找功能，限于篇幅，就不展开介绍了


##4.WebSql

Web SQL Database API实际上未包含在HTML 5规范之中，它是一个独立的规范，它引入了一套使用SQL操作客户端数据库的API，这些API有同步的，也有异步的，一般情况下，都会使用异步API。它的核心方法有三个：openDatabase，transaction和executeSql。这些API已经被广泛的实现在了不同的浏览器里，尤其是手机端浏览器。虽然W3C官方在2011年11月声明已经不再维护Web SQL Database规范，但由于其广泛的实现程度，了解这些API对 Web开发还是非常有必要的。

###浏览器兼容性
![WebSql浏览器兼容性](http://7xs3q2.com1.z0.glb.clouddn.com/websql_compatibility.png)
[详情请参考](http://caniuse.com/#search=WebSql)

###代码示例

```
var db; 
var info = {
    dbName :"MyDataBase",//数据库名称
    dbVersion:"0.1",//版本
    dbDisplayName:"测试数据库",//显示名称
    dbEstimatedSize:10*1024*1024 //数据库大小,单位字节
};

db = window.openDatabase(info.dbName,info.dbVersion,info.dbDisplayName,info.dbEstimatedSize);

//初始化students表
db.transaction(function (trans) {
    //执行Sql，如果students表不存在，则创建改表
    trans.executeSql("create table if not exists students(id unique,name text null,email text null)",[], function () {
        console.log("init success");
    }, function () {
        console.log("error happen");
    });
});


//插入数据
db.transaction(function (trans) {
	trans.executeSql("insert into students(name,email) values(?,?)",['xiaoming','1@qq.com'], function () {
	    console.log("insert ok 1");
	}, function () {
	    console.log(arguments);
	});
	trans.executeSql("insert into students(name,email) values(?,?)",['xiaohong','2@qq.com'],function () {
	    console.log("insert ok 2");
	}, function () {
	    console.log(arguments);
	});
});

//删除数据
db.transaction(function (trans) {
   trans.executeSql("delete from students where name = ? ",['xiaohong'], function (trans,result) {
       console.log("delete success");
   }, function (trans,message) {
       console.log("error happen");
   });
});

//查询数据
db.transaction(function (trans) {
    trans.executeSql("select * from students",[], function (trans,result) {
        console.log("总共查询到 "+result.rows.length+" 条数据");
    }, function (trans,message) {
        console.log("error happen");
    });
});

```

##5.其他
###Application Cache
Application Cache翻译成中文为应用程序缓存，是html5中为实现离线浏览所提供的API。结合Manifest文件使用，使用编程方式，更新浏览器缓存内容。主要调用update与swapCache去更新浏览缓存，目前该技术已经被最新的规范所废弃，转而使用了Service Workers。

###Service Workers
一个 service worker 是一段运行在浏览器后台进程里的脚本，它独立于当前页面，提供了一些不需要与web页面交互的功能，即那种在网页背后悄悄执行的能力。在将来，基于它可以实现消息推送，静默更新等服务，但是目前它首先要具备的功能是拦截和处理网络请求，包括可编程的响应缓存管理。

##小结

目前Cookie的兼容性最好，使用的最广泛，但有被滥用的趋势。Web Storage 兼容比较好，除了老板的IE 6，7不支持外，其他主流浏览器都已经支持了，使用起来也方便简单，适合存储键值对数据。WebSql由于未在HTML5规范中，前景堪忧，适当了解下。IndexDb目前来看，兼容性不太好，但是前景很好，目前由w3c在推广，相信在以后应该有个大爆发(个人看法)。
Application  Cache目前已经被废弃，Service Workers目前属于起步阶段，感觉离实用还需要时间。



###参考链接 
[caniuse](http://caniuse.com/)： http://caniuse.com/

[Cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)：https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie

[谷歌开发者中心文档](https://developer.chrome.com/devtools/docs/resource-panel#inspecting-page-resources)： https://developer.chrome.com/devtools/docs/resource-panel#inspecting-page-resources

[Mozilia 开发者中心](https://developer.mozilla.org/en-US/docs/Web)：https://developer.mozilla.org/en-US/docs/Web

[Service Workers](http://www.html5rocks.com/en/tutorials/service-worker/introduction/)：http://www.html5rocks.com/en/tutorials/service-worker/introduction/
	