# password_hash

Этот Golang пакет в роли аналога php функций password_hash и password_verify

Вам не нужно думать о хранении соли и других данных. Пакет делает это сам. Просто сохраните исходный хеш который вы получите.

Для начала работы нам необходимо установить наш пакет
```
go get github.com/vzglad-smerti/password_hash
```

Пример использования
```golang
package main

import (
	"log"

	"github.com/vzglad-smerti/password_hash"
)

func main() {
    //пароль который будем проверять
	password_users := "testing"

    //создадим хеш пароля
	hash, err := password.Hash(password_users)
	if err != nil {
		log.Print(err)
	}

    //сверим хем и пароль. Если верный пароль то вернёт true в противном случае false
	hash_veriry, err := password.Verify(hash, password_users)
	if err != nil {
		log.Print(err)
	}

    //выведем хеш в терминал
	log.Print(hash)
    //выведем результат проверки в терминал
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
