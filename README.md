struct-create
=============

Creates Go source file of structs for use in some MySQL database packages. It uses [go-sql-driver/mysql](https://github.com/go-sql-driver/mysql) for querying the information_schema database. I created this for personal use, so it's not written for extensibility, but shouldn't be difficult to adapt for your own use.

json tag is added

Configuration may be set in the source file:
```
var defaults = Configuration{
	DbUser: "db_user",
	DbPassword: "db_pw",
	DbName: "bd_name",
	// PKG_NAME gives name of the package using the stucts
	PkgName: "DbStructs",
	// TAG_LABEL produces tags commonly used to match database field names with Go struct
	//members. This will be skipped if the string is empty.
	TagLabel: "db",
}
```

Or by a JSON file using the json flag `struct-create --json=test.json`
```
{
	"db_user": "db_user",
	"db_password": "db_pass",
	"db_name": "db_name",
	"pkg_name": "JsonTest",
	"tag_label": "db"
}
```

Sample output file:
```
package DbStructs

import (
	"time"
	"database/sql"
)

type Audit struct{
	Id int64	`db:"id" json:"id"`
	User int64	`db:"user" json:"user"`
	Subject string	`db:"subject" json:"subject"`
	SubjectId int64	`db:"subject_id" json:"subject_id"`
	Action string	`db:"action" json:"action"`
	Content string	`db:"content" json:"content"`
	Created time.Time	`db:"created" json:"created"`
}

```
