## Cleverdeus 
Система построенная на основе передач данных по средствам TCP и Redis.

## Основа
 Приложение состоит из REST API модуля и микросервисов. 


## Environment setup

Обязательно установить среду окружения как в корневой папке так и в модулях микросервисов.
Для Мисросирвисов используются персональные настройки `.env` для каждого свои

<details>
<summary>Основные настройки окружения</summary>

создайте в корне директории файил `.env`и добавьте указанные ниже параметры
```bash
# Global variables
API_GATEWAY_PORT=4000
BASE_URI=http://localhost
JWT_SECRET=45e6adea-fd8e-40d7-a245-d0cc234e3ccf

## Brute force is used for auth endpoints
BRUTE_FREE_RETRIES = 50          # 50 requests
BRUTE_LIFETIME = 300000          #   in 5 mins

## Public limits
PUBLIC_RATE_LIMIT_MAX = 60       # 60 requests
PUBLIC_RATE_LIMIT_TIME = 60000   #    in 1 min
SPEED_LIMIT_COUNT = 500         # 1k requests
SPEED_LIMIT_TIME = 600000        #    in 1 min
SPEED_LIMIT_DELAY = 100          # delay 100ms

## Limits when using an API key
RATE_LIMIT_MAX = 1000            # 1k requests
RATE_LIMIT_TIME = 60000          #    in 1 min

# Mongodb
MONGO_DSN=mongodb://mongouserdb1:27017/cleverdeusdb
MONGO_HOST=192.168.56.100
MONGO_PORT=50001
MONGO_DATABASE=cleverdeusdb
MONGO_ENABLE=true
MONGO_USER=admin
MONGO_PASSWORD=23982y23f3hf3f37h3eh
MONGO_ROOT_USER=root
MONGO_ROOT_PASSWORD=knsdfs7845whdaHFFX

# Users Service
USER_SERVICE_PORT=4001
USER_SERVICE_HOST=127.0.0.1

# Profile Service
PROFILE_SERVICE_PORT=4002
PROFILE_SERVICE_HOST=127.0.0.1

# Customers Service
CUSTOMER_SERVICE_PORT=4003
CUSTOMER_SERVICE_HOST=127.0.0.1

# Mail Service
MAIL_SERVICE_PORT=5000
MAIL_SERVICE_HOST=127.0.0.1
MAIL_SERVICE_USER=no_reply@cleverdeus.com
MAIL_SERVICE_PASSWORD=02186eabe429WE
MAIL_SERVICE_SMTP=smtp.spaceweb.ru
MAIL_SERVICE_SMTP_PORT=465
MAIL_SERVICE_SMTP_TSL=true


```
</details>

## Docker setup

<details><summary>Установка в Docker</summary>

Перед запуском докера пожалуйста укажите правильно IP адреса для микросирвисов.

Из корневой директории в терминале выполните команду:
```bash
 docker-compose up -d
```

Для активации MongoDB Replica. В терминале докера выполните команду:
```bash
mongo mongodb://root:knsdfs7845whdaHFFX@192.168.56.100:50001?authSet=admin
```
IP адрес сервера укажите своего сервера на который будет установлен MongoDB

```js
rs.initiate(
  {
    _id: "shard1rs",
    members: [
      { _id : 0, host : "192.168.57.100:50001", priority: 1 },
      { _id : 1, host : "192.168.57.100:50002" },
      { _id : 2, host : "192.168.57.100:50003" }
    ]
  }
)
rs.status()
```
Таким образом вы укажите какой из серверов будет Primary
</details>