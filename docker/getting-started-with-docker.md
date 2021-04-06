# Getting started with Docker

* Cheatsheet: [https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf](https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf)

### Commands

```bash
# list all running docker processes
docker ps -a

1405023afa61   postgres:9.5-alpine                                 "docker-entrypoint.s…"   14 minutes ago   Up 14 minutes (healthy)   5432/tcp                 form3_postgresql_1
a6a41fe79816   vault:0.9.3                                         "docker-entrypoint.s…"   14 minutes ago   Up 14 minutes             8200/tcp                 form3_vault_1

# connect to a docker container interactively
docker exec -it 1405023afa61 bash 
```





