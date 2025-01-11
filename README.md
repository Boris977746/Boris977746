import uuid

# Укажите параметры VPN-сервера
SERVER_IP = "188.227.86.106"  # IP-адрес сервера
SERVER_PORT = 443  # Используемый порт
PUBLIC_KEY = "7132417386:AAEcrhVgsPV1ZX6CBvVZAKO7-cv1toBMKCM"  # Публичный ключ
SNI = "google.com"  # SNI-домен
SHORT_ID = "4c61c8b9920bb4b4"  # Краткий идентификатор (Short ID)
PATH = "/"  # Путь подключения

def generate_vless_link():
    """Функция для генерации корректной VLESS ссылки"""
    try:
        user_uuid = str(uuid.uuid4())  # Генерация UUID для пользователя
        
        # Формируем VLESS ссылку
        vless_link = (
            f"vless://{user_uuid}@{SERVER_IP}:{SERVER_PORT}"
            f"?type=tcp&security=reality&fp=chrome"
            f"&pbk={PUBLIC_KEY}&sni={SNI}&sid={SHORT_ID}&path={PATH}#VPN_User"
        )
        
        return vless_link
    except Exception as e:
        # Логирование ошибки
        print(f"Ошибка генерации ссылки: {e}")
        return None

# Тестируем
if __name__ == "__main__":  # Исправлено с name на __name__
    link = generate_vless_link()
    if link:
        print("Ваш VLESS URL: http://188.227.86.106:31155/vmwblSBJciiBhcA/panel/inbounds")
        print(link)


