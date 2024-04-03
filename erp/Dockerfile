FROM python:3.10-slim-bookworm

ENV UVICORN_PORT=8000 \
    UVICORN_HOST=0.0.0.0
VOLUME /app/config
ENTRYPOINT ["uvicorn", "asgi:app"]

# Устанавливаем SSH для того, чтобы установить пакеты из GitHub
# Ниже используется --mount=type=ssh для проброски SSH с хоста.
# Перед docker build нужно выполнить `eval $(ssh-agent) && ssh-add ~/.ssh/id_ed25519`. Также к build надо добавить `--ssh default=$SSH_AUTH_SOCK`
RUN apt-get update && \
    apt-get install -y --no-install-recommends openssh-client git && \
    mkdir -p -m 0700 ~/.ssh && \
    ssh-keyscan github.com >> ~/.ssh/known_hosts

WORKDIR /app
COPY ./requirements.txt ./

RUN --mount=type=ssh \
    pip install --no-cache-dir -r requirements.txt

COPY . .
