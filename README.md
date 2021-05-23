# Задание 

Backend for frontends. Apigateway

Цель:
В этом ДЗ вы научитесь добавлять в приложение аутентификацию и регистрацию пользователей.

Добавить в приложение аутентификацию и регистрацию пользователей.

Реализовать сценарий "Изменение и просмотр данных в профиле клиента". Пользователь регистрируется. Заходит под собой и по определенному урлу получает данные о своем профиле. Может поменять данные в профиле. Данные профиля для чтения и редактирования не должны быть доступны другим клиентам (аутентифицированным или нет).

На выходе должны быть:

0) описание архитектурного решения и схема взаимодействия сервисов (в виде картинки)
1) команда установки приложения (из helm-а или из манифестов). Обязательно указать в каком namespace нужно устанавливать. 1*) команда установки api-gateway, если он отличен от nginx-ingress.
2) тесты постмана, которые прогоняют сценарий:
 * регистрация пользователя 1
 * проверка, что изменение и получение профиля пользователя недоступно без логина
 * вход пользователя 1
 * изменение профиля пользователя 1
 * проверка, что профиль поменялся
 * выход* (если есть)
 * регистрация пользователя 2
 * вход пользователя 2
 * проверка, что пользователь2 не имеет доступа на чтение и редактирование профиля пользователя1.

В тестах обязательно:
 * наличие {{baseUrl}} для урла
 * использование домена arch.homework в качестве initial значения {{baseUrl}}
 * использование сгенерированных случайно данных в сценарии
 * отображение данных запроса и данных ответа при запуске из командной строки с помощью newman.

# Подготовка среды
## Вырубить валидацию для ingress
```
kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission
```

# Порядок установки
* postgres
* otus-auth
* otus-user
* otus-api-gateway
* nginx-ingress

## postgres
```
helm install postgres bitnami/postgresql -f ./postgres/values.yaml -n otus
```

## otus-auth
```
helm install otus-user ./otus-auth/otus-auth-chart -f ./otus-auth/values.yaml -n otus
```
## otus-user
```
helm install otus-user ./otus-user/otus-user-chart -f ./otus-user/values.yaml -n otus
```
## otus-api-gateway
```
helm install otus-api-gateway ./otus-api-gateway/otus-api-gateway-chart -f ./otus-api-gateway/values.yaml -n otus
```
## nginx-ingress


# Api-тесты из Postman 
Предварительно необходимо изменить хост arch.homework на ip ingress'а или изменить дефолтный в user_api_postman_collection.json

```newman run tests/API_Gateway_Tests.postman_collection.json```
