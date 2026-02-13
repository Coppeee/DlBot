Установка на VDS Ubuntu (20.04/22.04/24.04)

1) Установить Docker + Compose plugin
apt update
apt install -y ca-certificates curl gnupg
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" \
  > /etc/apt/sources.list.d/docker.list
apt update
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

2) Развернуть в /root/dlbot
mkdir -p /root/dlbot
cd /root/dlbot
# загрузить архив и распаковать
unzip dlbot_full_release.zip

3) Настроить .env
cp .env.example .env
nano .env

  Заполни обязательно:
    BOT_TOKEN — токен от @BotFather
    ADMIN_ID — твой Telegram user id
    TELEGRAM_API_ID и TELEGRAM_API_HASH — для локального Bot API (получить тут: https://core.telegram.org/api/obtaining_api_id)

4) Запуск
cd /root/dlbot
docker compose -p dlbot up -d --build
docker compose -p dlbot ps

Логи
docker logs -f dlbot-bot-1
docker logs -f dlbot-tg-bot-api-1
