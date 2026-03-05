## Создание сервера GRPC

[GRPC documentations](https://grpc.io/docs/languages/python/quickstart/)

### Первый этап - написание прото файла, генерация серверной части, описание заготовки самого сервиса

- Создали proto файл
- установить библиотеку grpcio-tools
- сгенерировать код по прото файлу - создание папки internal

```commandline
python -m grpc_tools.protoc -I./protos --python_out=./internal/pb --pyi_out=./internal/pb --grpc_python_out=internal/pb ./protos/photocatalog.proto
```

- описываем заготовку сервиса - создаем пакет с приложением `app/service/photocatalog`

### Второй этап создание Mock репозитория для эмуляции логики входа

- создание файла `mock_repository` и создание класса `MockRepository`

### Запуск локального gRPC сервера

- создаем файл `protocol` для репозитория описываем какие методы он должен содержать
- более подробно определяем функции в файле `service`
- получение фото
- добавление фото
- добавление фото в стрим режиме

Запустить сервер из файла `main.py`

### Проверка работы сервиса

В программе `Postman` осуществить отправку сообщений по добавлению Фото в стрим режиме используя тестовое сообщение.
port `0.0.0.0:50051`

- Импортируем протофайл в Postman, указав путь до нашего файла. gRPC предоставляет возможность reflection API - в
  сервере объявляем название сервиса и кладем туда дескриптор и подключаем его - библиотека `grpc-reflection`:
```python
from grpc_reflection.v1alpha import reflection

    SERVICE_NAMES = (
  photocatalog_pb2.DESCRIPTOR.services_by_name[
    "PhotoCatalogService"
  ].full_name,
  reflection.SERVICE_NAME,
)
```
- После подгрузки файла будут доступны методы из `MockRepository`
- Формируем тестовое сообщение, например

```json
{
  "content": "fugiat dolor",
  "description": "nulla veniam deserunt esse amet"
}
```

