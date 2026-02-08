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

### Второй этап 