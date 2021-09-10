需要，因为事务的边界不在 DAO 层上，而是在service 层上，



```
DAO层:
import (
	"database/sql"
	"github.com/pkg/errors"
)

type User struct {
	Id int
	Name string
	Sex int
}

var Db sql.DB

func GetUserName(id int) (string, error)  {
	var name string
	err := Db.QueryRow("select name from User where id = ?", id).Scan(&name)
	if err != nil {
		return name, errors.Wrap(err, "GetUserInfo err")
	}

	return name, nil
}

service层: 
userName, err := dao.getUserName(id)
if errors.Is(err, sql.ErrNoRows) {
	fmt.Printf("no user")
}
```

