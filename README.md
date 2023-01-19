### Components

- todolist-flask: backend
- todolist-vue: frontend
- redis: db

### Usage

```
docker-compose up --build
```

Or run with `-d` in detached mode, then visit `http://localhost:8080/`.

Also check the dockerfiles in the subdirectories.

### TODO

- Port to kubernetes. Currently it's just docker containers.
- User auth/login. Do we need this?
- Scalability. Currently there's 3 containers: redis, node and flask. Probably need to change the code if server scales.
- Make frontend prettier.
- Network stuff. e.g., SSL, hardcoded config like ports and addresses.

