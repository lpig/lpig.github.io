---
layout: post
title:  "新手用go语言操控mysql数据库时可能遇到的问题"
date:  2015-08-12  16:13
tags:
  - golang
  - mysql
---

新手用go操控mysql数据库时可能遇到的问题：
最近在弄go操控数据库时遇到了一个问题，其实是一个很小的问题，不过当初按照一般的惯性思维来理解弄的话就出现错误了。
首先先从一开始说起：

```go
package main

import (
	"database/sql"
	"fmt"
	_ "github.com/go-sql-driver/mysql"
	"log"
)

func main() {

	db, err := sql.Open("mysql", "root:123456@/test")
	defer db.Close()

	if err != nil {
		log.Fatalf("Open database error: %s\n", err)
	}
	err = db.Ping()
	if err != nil {
		log.Fatalf("ping database error: %s\n", err)
	}

	// insert(db)
	selectDB(db)
	fmt.Println("OK")

}

func selectDB(db *sql.DB) {
	rows, err := db.Query("select * from t_user")
	if err != nil {
		log.Println(err)
	}

	defer rows.Close()
	// var id int
	var name string
	for rows.Next() {
		err := rows.Scan(&name)
		if err != nil {
			log.Fatal(err)
		}
		fmt.Println(name)
	}

	err = rows.Err()
	if err != nil {
		log.Fatal(err)
	}
}
```

这个代码咋看之下好像没有什么大的问题，而且SQL语句也可以查询，但是编译运行就报错了：
![enter image description here](http://7xkxs2.com1.z0.glb.clouddn.com/sqlerror.png)
上面的意思是，select查出来有三个变量但是rows.Scan里面就只有一个变量来接受，所以编译就报错了，解决办法也是很简单，只要把查出来的东西都找变量装起来或者不要查那么多就好了。
```go
func selectDB(db *sql.DB) {
	rows, err := db.Query("select id,name from t_user")
	if err != nil {
		log.Println(err)
	}

	defer rows.Close()
	var id int
	var name string
	for rows.Next() {
		err := rows.Scan(&id, &name)
		if err != nil {
			log.Fatal(err)
		}
		fmt.Printf("id:%d,name:%s\n", id, name)
	}

	err = rows.Err()
	if err != nil {
		log.Fatal(err)
	}
}
```


于是问题就解决了：
![enter image description here](http://7xkxs2.com1.z0.glb.clouddn.com/sqlok.png)

**随便一提的是，rows.Scan里面存放变量的顺序一定要和查的时候的顺序对应。**
