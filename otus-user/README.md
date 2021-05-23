# otus-sa-hw3
Helm-chart для разворачивания demo-сервиса. Имеет в зафисимостях postgres chart из bitnami repo. 
Java-сервис с sql-миграциями на Flyway, поэтому время старта зависит от полного поднятия postgres. 

## Старт
```helm install otus-demo ./otus-demo-chart -f values.yaml```

## Тест
```curl http://arch.homework/otusapp/vtimoshenko/health```
  
## Api-тесты из Postman 
Предварительно необходимо изменить хост на ip ingress'а в user_api_postman_collection.json или прописать в хосты arch.homework  

```newman run tests/user_api_postman_collection.json```

Нагрузка:
```./tests/perfomance_test.sh```  
