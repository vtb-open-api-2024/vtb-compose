# vtb-compose

```bash
# build backend app
$ docker build -t vtb-backend .

# check that app works
$ docker run --env-file .env -d -p 3000:3000 vtb-backend

# build all backend
$ docker-compose up --build
```
