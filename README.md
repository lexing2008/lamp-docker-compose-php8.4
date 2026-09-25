# lamp-docker (Linux + Apache + MariaDB + PHP)

### Настройка 
#### 1. Нужно добавить в /etc/hosts

```
127.0.0.1   domain.local
```

```
sudo nano /etc/hosts
```
#### 2. Добавить папку /www и в нее спуллить репозиторий


### Полезные команды
Запустить контейнеры
```
docker compose up -d
```
Остановить контейнеры
```
docker compose down
```
Сборка проекта
```
docker compose build
```
Войти в контейнер
```
docker compose exec <имя контейнера> bash
docker compose exec db bash
docker compose exec imgproxy bash
docker compose exec apachephp bash
```
Просмотреть лог контейнера
```
docker compose logs <имя контейнера>
docker compose logs imgproxy 
docker compose logs apachephp
```
Остановить, пересобрать и запустить контейнеры
```
docker compose down && docker compose build && docker compose up -d
```

Run migrations
```
docker compose exec apachephp php artisan migrate
```

Изменить владельца папок и файлов
```
sudo chown -R $USER:$USER ./www
sudo chmod -R 755 ./www
```
