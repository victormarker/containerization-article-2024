Для сборки и запуска приложения используйте следующие команды:

1. Запустить сессию SSH-агента 
   ```bash
   eval $(ssh-agent)
   ssh-add ~/.ssh/id_ed25519
   ```
2. Выполнить сборку набора контейнеров
   ```bash
   docker-compose build –ssh default=$SSH_AUTH_SOCK
   ```
3. Запустить нобор контейнеров в фоне
   ```bash
   docker-compose up -d
   ```
