import telebot
import uuid

# Укажите API-ключ вашего бота
BOT_TOKEN = "7132417386:AAEcrhVgsPV1ZX6CBvVZAKO7-cv1toBMKCM"
bot = telebot.TeleBot(BOT_TOKEN)

# Данные вашего VPN-сервера
SERVER_ADDRESS = "http://188.227.86.106:31155/vmwblSBJciiBhcA/panel/inbounds"  # Ваш домен или IP
SERVER_PORT = 443  # Порт сервера
PROTOCOL_TYPE = "vless://8e87ae3c-a567-4344-9cae-07b085ceca1e@188.227.86.106:443?type=tcp&security=reality&pbk=EK0DL1OIO6JDEAIME2sxcn7HauznNO_IsPDdXpMmxRw&fp=chrome&sni=google.com&sid=4c61c8b9920bb4b4&spx=%2F#1S-1S"  # Можно использовать vless, vmess, trojan и т.д.

# Приём команды /start
@bot.message_handler(commands=["start"])
def send_welcome(message):
    bot.reply_to(
        message,
        "👋 Добро пожаловать в VPN-бота!\n\n"
        "Для получения конфигурации VPN нажмите на команду /get_vpn."
    )

# Генерируем VPN-конфигурацию
@bot.message_handler(commands=["get_vpn"])
def generate_vpn(message):
    user_id = uuid.uuid4()  # Уникальный UUID для пользователя
    config_link = f"{PROTOCOL_TYPE}://{user_id}@{SERVER_ADDRESS}:{SERVER_PORT}?encryption=none#VPN-User"
    
    bot.reply_to(
        message,
        f"🎉 Ваше подключение готово!\n\n"
        f"Скопируйте ссылку ниже и используйте её в VPN-клиенте:\n"
        f"```\n{config_link}\n```",
        parse_mode="Markdown"
    )

# Запускаем бота
bot.polling()

