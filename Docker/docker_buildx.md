

### 1. Borrar el caché de Buildx directamente

`docker buildx prune`

- Te pedirá confirmación para borrar el caché de _todas_ las builds.
- Si quieres forzarlo sin preguntar:

`docker buildx prune -f`

Para borrar también las capas que ya no están referenciadas:

`docker buildx prune -af`

(`-a` = all, no solo caché no usado recientemente).

---

### 2. Borrar caché de un builder específico

Ya que en tu `docker buildx ls` aparecen dos (`default` y `desktop-linux`), puedes limpiar uno en particular:

`docker buildx use desktop-linux docker buildx prune -af`

Luego puedes volver al otro builder si lo deseas:

`docker buildx use default`

---

### 3. Limpiar caché de volúmenes BuildKit manualmente

En casos donde BuildKit se queda “atascado”, puedes eliminar los volúmenes asociados:

`docker volume ls | grep buildx_buildkit docker volume rm $(docker volume ls -q | grep buildx_buildkit)`

Esto forzará la recreación completa del caché en la siguiente build.

---

### 4. Forzar que una build no use caché

Si lo que quieres es solo que **la siguiente build se reconstruya desde cero**:

`docker buildx build --no-cache -t miimagen:latest .`

---


✅ **Recomendación**: pon en tu `~/.zshrc`:

```
export DOCKER_BUILDKIT=1
export BUILDKIT_PROGRESS=tty
```


Pushar las imagenes

```
docker compose push pentest-arm
docker compose push pentest-amd

docker push hackadvisermx/pentest:multi-arch

```

## en mi .zshrc

```

## Ahora que uso docker compose , puedo simplificar mis alias

# Construcción de las imágenes con compuse
alias pdb-arm="cd ~/ptd && docker compose --profile arm build"
alias pdb-amd="cd ~/ptd && docker compose --profile amd build"

# construccion de imagenes directo para tener colores y usar buildx
alias pdb-amd-c="cd ~/ptd && docker buildx build \
  --file docker-pentest \
  --platform linux/amd64 \
  --progress=tty \
  --tag pentest:amd64  --load \
  ."

alias pdb-arm-c="cd ~/ptd && docker buildx build \
  --file docker-pentest \
  --platform linux/arm64 \
  --progress=tty \
  --tag pentest:arm64  --load \
  ."

alias pdb-multi-arch="cd ~/ptd && docker buildx build \
  --file docker-pentest \
  --platform linux/amd64,linux/arm64 \
  --progress=tty \
  --tag pentest:multi-arch --load \
  ."

# Construcción de los contenedores
alias pdr-arm="cd ~/ptd && docker compose --profile arm -f docker-compose.yml up -d pentest-arm && docker exec -it pentest-arm /bin/zsh && docker compose --profile arm -f docker-compose.yml down"
alias pdr-amd="cd ~/ptd && docker compose --profile amd -f docker-compose.yml up -d pentest-amd && docker exec -it pentest-amd /bin/zsh && docker compose --profile amd -f docker-compose.yml down"

export DOCKER_BUILDKIT=1
export BUILDKIT_PROGRESS=tty
```