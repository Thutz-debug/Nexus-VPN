# Nexus-VPN
# 🌐 Universal VPN Client (Linux & Windows)

    <p align="center">
      <img src="https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-blue?style=for-the-badge&logo=linux&logoColor=white" alt="Platforms" />
      <img src="https://img.shields.io/badge/Core-sing--box%20v1.14-orange?style=for-the-badge" alt="sing-box" />
      <img src="https://img.shields.io/badge/Protocols-VLESS%20%7C%20Shadowsocks%20%7C%20Trojan%20%7C%20VMess-success?style=for-the-badge" alt="Protocols" />
      <img src="https://img.shields.io/badge/Mode-TUN%20(VPN)%20%7C%20Proxy-purple?style=for-the-badge" alt="Modes" />
    </p>

    Готовый к работе портативный VPN-клиент для **Linux** и **Windows** с поддержкой современных протоколов обхода блокировок: **VLESS** *(XTLS Reality / Vision / WebSocket / gRPC)*, **Shadowsocks** *(2022 / AEAD)*,
  **Trojan** и **VMess**.

    Включает предсобранные бинарные файлы ядра **sing-box**, TUN-драйверы, скрипты запуска в 1 клик и автоматический парсер ссылок подключения.

    ---

    ## ⚡ Особенности

    - 🚀 **Работа «из коробки»**: бинарники и драйверы уже внутри репозитория, ничего не нужно компилировать.
    - 🔗 **Умный импорт ссылок**: парсит `vless://`, `ss://`, `trojan://`, `vmess://` и мгновенно создает рабочий `config.json`.
    - 🛡 **Полноценный TUN-режим**: направляет весь интернет-трафик системы (игры, браузеры, консоль, любые приложения) через VPN.
    - 🔀 **Режим локального прокси**: работа без прав администратора/root (SOCKS5/HTTP на `127.0.0.1:2080`).
    - 🪟 **Удобство для Windows**: интерактивное меню и запуск в 1 клик через `.bat` файлы с автоповышением прав.
    - 🐧 **Удобство для Linux**: интерактивные скрипты запуска, фоновый режим и шаблон службы `systemd`.

    ---

    ## 📂 Структура репозитория

    ```text
    ├── linux/                  # Платформа Linux
    │   ├── bin/sing-box        # Исполняемый файл sing-box (x86_64)
    │   ├── client.py           # CLI утилита (импорт ссылок, TUN / Proxy)
    │   ├── start.sh            # Скрипт запуска (интерактивный или с флагами)
    │   ├── stop.sh             # Быстрая остановка процесса
    │   ├── status.sh           # Проверка статуса и тест соединения
    │   ├── config.json         # Файл конфигурации
    │   └── README.md           # Подробное руководство по Linux
    │
    └── windows/                # Платформа Windows
        ├── bin/sing-box.exe    # Портативный sing-box.exe
        ├── bin/wintun.dll      # Драйвер высокопроизводительного интерфейса WinTun
        ├── start.bat           # Меню управления в 1 клик
        ├── start-tun.bat       # Запуск полного VPN (TUN)
        ├── start-proxy.bat     # Запуск с автонастройкой системного прокси
        ├── stop.bat            # Остановка и сброс настроек
        ├── status.bat          # Проверка статуса процесса
        ├── client.py           # CLI утилита
        ├── config.json         # Файл конфигурации
        └── README.md           # Подробное руководство по Windows
  ──────
  ## 🐧 Быстрый старт: Linux

  ### 1. Импорт ссылки подключения

    cd linux
    python3 client.py import "vless://ВАША_ССЫЛКА..."

  (Скрипт автоматически распознает Reality/TLS ключи, UUID, порты и создаст валидный config.json).

  ### 2. Запуск подключения

  • Режим полного VPN (TUN, весь трафик системы):
    sudo ./start.sh tun

  • Режим локального прокси (без root, порт 127.0.0.1:2080):
    ./start.sh proxy

  • Или через интерактивное меню:
    ./start.sh


  ### 3. Управление

    ./status.sh            # Проверить статус, PID и внешний IP
    ./stop.sh              # Остановить работу клиента
    tail -f sing-box.log   # Просмотр логов в реальном времени
  ──────
  ## 🪟 Быстрый старт: Windows

  ### 1. Добавление конфигурации

  • Через ссылку (если установлен Python):
    cd windows
    python client.py import "vless://ВАША_ССЫЛКА..."

  • Или вручную:
  Отредактируйте файл windows\config.json, вставив параметры вашего сервера.

  ### 2. Запуск в 1 клик

  Запустите нужный .bat файл двойным кликом:

   Файл                                                      │ Режим                                                    │ Описание
  ───────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────
   start-tun.bat                                             │ Полный VPN                                               │ Направляет весь интернет-трафик Windows через VPN. Автоматически запрашивает права Администратора.
   start-proxy.bat                                           │ Системный прокси                                         │ Запускает локальный прокси и включает прокси в настройках Windows для всех браузеров.
   start.bat                                                 │ Меню                                                     │ Главное окно управления всеми функциями.
   stop.bat                                                  │ Остановка                                                │ Останавливает процесс и возвращает стандартные сетевые настройки.
  ──────
  ## 🖥 Рекомендуемые графические клиенты (GUI)

  Если вам нужно классическое оконное приложение с иконкой в трее:

   Клиент                                                                  │ Платформы                                                              │ Ссылки и команды установки
  ─────────────────────────────────────────────────────────────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────────────────────────────────────────────────────────────
   Hiddify[1] (Рекомендуется)                                              │ Windows, Linux, Android, iOS, macOS                                    │ Windows: winget install Hiddify.HiddifyLinux: AppImage Releases[2]
   v2rayN[3]                                                               │ Windows                                                                │ GitHub Releases[4] (скачивать архив With-Core)
   NekoRay[5]                                                              │ Windows, Linux                                                         │ GitHub Releases[6]
   v2rayA[7]                                                               │ Linux (Web GUI)                                                        │ Документация v2rayA[8]

  [1]: Hiddify https://github.com/hiddifynet/hiddify-app
  [2]: AppImage Releases https://github.com/hiddifynet/hiddify-app/releases
  [3]: v2rayN https://github.com/2dust/v2rayN
  [4]: GitHub Releases https://github.com/2dust/v2rayN/releases
  [5]: NekoRay https://github.com/MatsuriDayo/nekoray
  [6]: GitHub Releases https://github.com/MatsuriDayo/nekoray/releases
  [7]: v2rayA https://github.com/v2rayA/v2rayA
  [8]: Документация v2rayA https://v2raya.org/
  ──────
  ## 🔒 Безопасность и конфиденциальность

  • Репозиторий использует исключительно открытое и проверенное ядро sing-box https://github.com/SagerNet/sing-box и драйвер WinTun https://www.wintun.net/.
  • Никакой телеметрии и сторонних серверов: соединение идет напрямую на ваш сервер.
  • Поддерживается маскировка трафика под обычный HTTPS (VLESS Reality / Vision / uTLS Chrome).
  ──────
  ## 📄 Лицензия

  MIT License. Исходный код ядра sing-box распространяется под лицензией GPL-3.0.

