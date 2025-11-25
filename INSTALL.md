# **Мини-инструкция по установке snx-rs (v4.9.2astra)**

На странице [релиза](https://github.com/dmtnndxr/snx-rs/releases/tag/v4.9.2astra) доступны два варианта:

* **tar.xz** — архив с бинарями и скриптом `install.sh` (устанавливается вручную).
* **.run** — самораспаковывающийся инсталлятор (тот же набор файлов), автоматически запускает `install.sh` и требует root.

Мы установим вариант **.run**.

---

## **1. Скачиваем инсталлятор**

```bash
wget https://github.com/dmtnndxr/snx-rs/releases/download/v4.9.2astra/snx-rs-v4.9.2astra-linux-x86_64.run
```

## **2. Делаем файл исполняемым**

```bash
chmod +x snx-rs-v4.9.2astra-linux-x86_64.run
```

## **3. Запускаем установку (требует root)**

```bash
sudo ./snx-rs-v4.9.2astra-linux-x86_64.run
```

Инсталлятор сам распакует содержимое и выполнит `install.sh`.
Программа будет доступна в меню приложений как **SNX-RS VPN client**.

## 4. Устанавливаем зависимости

Для запуска GUI-клиента потребуется дополнительная библиотека `libgtk-4-1`.

```bash
sudo apt install libgtk-4-1
```

## **5. (Опционально) вынести ярлык на рабочий стол**

```bash
cp /usr/share/applications/snx-rs-gui.desktop ~/Desktop/
```
