## Что понадобится

- Банковская карта (Visa/MC/МИР)
- ~10–15 минут времени
- SSH-клиент: [Termius](https://termius.com/) (Desktop/Mobile) или встроенный терминал (Mac/Linux), PuTTY (Windows)

---

## 1. Выбираем хостинг и берём VPS

Ниже — лично проверенные провайдеры. Рекомендуется брать **минимальный тариф** (1 CPU / 1 GB RAM / 20 GB SSD), этого хватит с запасом.

| Провайдер                                                                                       | Особенности                            | Ссылка                                        |
| ----------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------- |
| **HostKey**                                                                                     | Нидерланды/США, оплата картой и крипто | [hostkey.com](https://hostkey.com/)           |
| **Xorek Cloud (Фаворит - у остальных через ~недели скорость падала, скорее всего блокали РКН)** | Европа, дешёвые тарифы, быстрый старт  | [xorek.cloud](https://xorek.cloud/en)         |
| **Fornex**                                                                                      | Русскоязычный саппорт, оплата МИР      | [ru.fornex.com](https://ru.fornex.com/)       |
| **U1Host**                                                                                      | Европа, гибкие конфигурации, Cloud VPS | [u1host.com](https://u1host.com/en#cloud-vps) |

### Что выбирать при заказе

- **ОС:** Ubuntu 22.04 LTS (рекомендуется)
- **Регион:** любой за пределами РФ (Нидерланды и Германия (Центральная россия), Финляндия (Питер и окрестности))
- **Доступ:** SSH с паролем или ключом — оба варианта подходят

После оплаты получишь на почту: **IP-адрес**, **логин** (`root`) и **пароль**.

---

## 2. Подключаемся к серверу

```bash
ssh root@ВАШ_IP
```

Либо добавляешь коннект через termius
![[Guide.png]]

Вводишь пароль из письма. Готово — ты на сервере.

---

## 3. Выбери протокол и установи

### Вариант A — Hysteria2 (быстрый, хорошо обходит блокировки)

Репозиторий: [github.com/ReturnFI/Blitz](https://github.com/ReturnFI/Blitz)

Hysteria2 работает по протоколу QUIC/UDP — очень быстрый и плохо детектируется.

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/ReturnFI/Blitz/main/install.sh)
```

После запуска скрипт задаст вопросы (порт, пароль и т.д.). Отвечай на подсказки, в конце получишь **ссылку-конфиг** вида `hysteria2://...` — добавь её в клиент (см. таблицу ниже).

---

### Вариант B — VLESS через 3x-ui (панель с веб-интерфейсом)

Репозиторий: [github.com/MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)

3x-ui — удобная веб-панель для управления несколькими пользователями и протоколами (VLESS, VMess, Trojan).

```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

После установки скрипт выведет:

- Адрес панели: `http://ВАШ_IP:2053/`
- Логин и пароль

Заходишь в браузере, создаёшь **inbound** (вкладка «Inbounds» → «Add Inbound»):

- Protocol: `VLESS`
- Network: `TCP` или `WebSocket`
- TLS: включить, выбрать Reality или TLS

Нажимаешь на значок QR-кода у созданного сервера — получаешь ссылку для клиента (см. таблицу ниже).

---

## Клиенты

### ПК (Windows / macOS / Linux)

| Клиент      | Протоколы                      | Примечание                         | Ссылка                                                                   |
| ----------- | ------------------------------ | ---------------------------------- | ------------------------------------------------------------------------ |
| **Happ**    | VLESS, Hysteria2, VMess и др.  | Удобный, современный UI            | [happ.tech](https://happ.tech/)                                          |
| **Throne**  | VLESS, Hysteria2, Trojan и др. | Лёгкий, быстрый старт              | [thronevpn.com](https://thronevpn.com/)                                  |
| **Nekoray** | VLESS, VMess, Hysteria2 и др.  | Больше не обновляется, но стабилен | [github.com/MatsuriDayo/nekoray](https://github.com/MatsuriDayo/nekoray) |
| **Hiddify** | VLESS, Hysteria2, Trojan и др. | Открытый код, активно развивается  | [hiddify.com](https://hiddify.com/)                                      |
| **v2rayN**  | VLESS, VMess, Hysteria2 и др.  | Классика, много настроек           | [github.com/2dust/v2rayN](https://github.com/2dust/v2rayN)               |

### Телефон (Android / iOS)

| Клиент           | Платформа     | Протоколы                | Примечание                          | Ссылка                                                                                       |
| ---------------- | ------------- | ------------------------ | ----------------------------------- | -------------------------------------------------------------------------------------------- |
| **Happ**         | Android / iOS | VLESS, Hysteria2 и др.   | Тот же клиент что и на ПК           | [happ.tech](https://happ.tech/)                                                              |
| **v2rayTUN**     | Android / iOS | VLESS, VMess, Hysteria2  | Простой и надёжный                  | [GitHub](https://github.com/vfarid/v2ray-tun)                                                |
| **V2rayNG**      | Android       | VLESS, VMess, Hysteria2  | Самый популярный на Android         | [github.com/2dust/v2rayNG](https://github.com/2dust/v2rayNG)                                 |
| **Hiddify**      | Android / iOS | VLESS, Hysteria2 и др.   | Открытый код, прост в настройке     | [hiddify.com](https://hiddify.com/)                                                          |
| **NekoBox**      | Android       | VLESS, Hysteria2, Trojan | Гибкий, поддерживает много ядер     | [github.com/MatsuriDayo/NekoBoxForAndroid](https://github.com/MatsuriDayo/NekoBoxForAndroid) |
| **Shadowrocket** | iOS           | VLESS, VMess, Hysteria2  | Платный ($2.99), лучший на iPhone   | App Store                                                                                    |
| **Streisand**    | iOS           | VLESS, Hysteria2 и др.   | Бесплатный альтернатив Shadowrocket | App Store                                                                                    |

> **Совет:** Импорт конфига везде одинаковый — скопируй ссылку (`vless://...` или `hysteria2://...`) и вставь в приложение, либо отсканируй QR-код из панели 3x-ui.

---

## 4. Базовая безопасность (займёт 2 минуты)

```bash
# Обновить систему
apt update && apt upgrade -y

# Сменить SSH-порт (опционально, но снижает брутфорс)
nano /etc/ssh/sshd_config
# Найти строку: #Port 22 → изменить на Port 2222
systemctl restart ssh
```

> !!! После смены порта подключайся через `ssh root@IP -p 2222`

---

## 5. Быстрая шпаргалка

| Действие             | Команда                       |
| -------------------- | ----------------------------- |
| Статус Hysteria2     | `systemctl status hysteria2`  |
| Перезапуск Hysteria2 | `systemctl restart hysteria2` |
| Статус 3x-ui         | `x-ui status`                 |
| Перезапуск 3x-ui     | `x-ui restart`                |
| Логи 3x-ui           | `x-ui log`                    |

---

## Частые вопросы

**Нужен ли домен?**
Нет, для базовой работы достаточно IP. Домен нужен только для TLS-сертификата (можно получить бесплатно через Let's Encrypt, 3x-ui умеет это делать сам).

**Один VPS — несколько человек?**
Да, 3x-ui позволяет создавать отдельные ключи для каждого пользователя с лимитами трафика.

**Что быстрее — Hysteria2 или VLESS?**
Hysteria2 быстрее на слабых каналах и при высоком пинге. VLESS надёжнее там, где UDP блокируется.
