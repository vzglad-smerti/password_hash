# password_hash

Этот Golang пакет в роли аналога php функций password_hash и password_verify

Для начала работы нам необходимо установить наш пакет
```
go get github.comvzglad-smerti/password_hash
```

Пример использования
```golang
import (
  "github.com/v-smerti/password"
  "log"
)

func main() {
    pass_users := "тест"
		
		//генерация хеша от пароля
		hash, err := password.Hash(pass_users)
		if err != nil {
			log.Print(err)
		}
		//наш хеш
    log.Print(hash)
		
		//Сверим хеш и пароль. Если пароль верный вернёт true в противном случае false. 
		hash_veriry, err := password.Verify(hash, "testing")
		if err != nil {
			log.Print(err)
		}
		log.Print(hash_veriry)
	}
```

Настройки хеширования производятся в коде самого пакета
```golang
const (
	saltSize            = 16    //размер соли
	delmiter            = "$#$" //строка с помощью которой в хеше разбиваться соль1, соль2, хеш и т.д.
	stretching_password = 500   //по сколько раз хешировать пароль алгоритмами sha256 и sha512 
	salt_local_secret   = "ahfw*&TGdsfnbi*^Wt" //локальная соль. Не где не передаётся 
)
```
