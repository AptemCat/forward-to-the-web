# Проведите всё что угодно в открытый интернет

Инструкция, о том как выводить сервера и порты с локалхоста прямо в интернет без лишних затрат.

1. [Вступление](#вступление)  
2. [Установка и настройка](#установка-и-настройка)  
   1. [Windows](#windows)  
   2. [Linux](#linux)  
   3. [Mac OS](#mac-os)
3. [Использование](#использование)

## Вступление

Мы будем использовать связку TempMail+ngrok, TempMail создаст нам почту для аккаунта на ngrok, которую можно сразу же уничтожить после подтверждения аккаунта, т.к. она нам не нужна.

## Установка и настройка

### Windows

Скачайте с [сайта](https://ngrok.com/download) архив, соответствующий архитектуре вашего ПК. Этот сайт покажет вам требуемый архив на кнопке загрузки и вам не потребуется выбирать, но если все-таки придётся, нажмите на кнопку "More options" и выберите вашу архитектуру. После загрузки разархивируйте файл куда-либо.

### Linux

На Linux есть два варианта установки: архив(см. [инструкцию для Windows](#windows)), или через snap.
Если вы выбрали вариант с snap, вам нужно сначала его установить:

```shell
sudo apt install snapd
sudo ln -s /var/lib/snapd/snap /snap
```
Затем установите сам ngrok:
```shell
sudo snap install ngrok
```

### Mac OS

Установка только через homebrew:
```shell
brew cask install ngrok
```
---
Теперь самое интересное. Эта процедура общая для всех ОС.  
Зайдите на [сайт](http://temp-mail.org/ru/). Вы сразу получите временный адрес электронной почты, по типу "janipo7484@ofdow.com". Скопируйте его, он нам пригодится.  
Пройдите по [ссылке](http://dashboard.ngrok.com/signup), зарегистрируйтесь, используя ранее скопированную почту и любой пароль.  
Вы увидите страницу с инструкциями по установке. Пролистайте до пункта "2. Connect your account". Здесь вы увидите команду, что-то вроде ```./ngrok authtoken 1ksxw9hF3rSYAuvmKk2TDx7qXEx_33xiuLEn2Lf64jncyZjVX```.  
Сейчас важная информация! Если вы устанавливали ngrok **через архив**, то войдите в папку в которую вы распаковали архив, введите команду как есть в командную строку/терминал. Если вы устанавливали ngrok **через менеджер пакетов**, уберите у команды "./" спереди. То есть например вот так: ```ngrok authtoken 1ksxw9hF3rSYAuvmKk2TDx7qXEx_33xiuLEn2Lf64jncyZjVX```. Не забудьте! Это будет влиять и **при использовании команды.**

## Использование

Допустим у вас есть веб сервер на порту 80, и вы хотите провести его в интернет. Вот команда:
```shell
ngrok http 80
```
Вы получите экран:  
ngrok by @inconshreveable        (Ctrl+C to quit)  
  
Session Status                online  
Account                       your@email.com (Plan: Free)  
Version                       2.3.35  
Region                        United States (us)  
Web Interface                 http://127.0.0.1:4040  
Forwarding                    **http://89c841e72567.ngrok.io** -> http://localhost:80  
Forwarding                    https://89c841e72567.ngrok.io -> http://localhost:80  
  
Connections                   ttl     opn     rt1     rt5     p50     p90  
                              0       0       0.00    0.00    0.00    0.00  
Ваш сервер теперь находится в интернете по адресу http://89c841e72567.ngrok.io.

---
Другой случай. У вас есть сервер протокола TCP: обычный TCP, SSH, FTP или другие виды сервера, не являющиеся HTTP сервером. Он находится на порту 1234. Вот команда для этого случая:
```shell
ngrok tcp 1234
```
Вы увидите следующий экран:  
ngrok by @inconshreveable                             (Ctrl+C to quit)  
  
Session Status                online  
Account                       your@email.com (Plan: Free)  
Version                       2.3.35  
Region                        United States (us)  
Web Interface                 http://127.0.0.1:4040  
Forwarding                    **tcp://2.tcp.ngrok.io:17018** -> localhost:1234  
  
Connections                   ttl     opn     rt1     rt5     p50     p90  
                              0       0       0.00    0.00    0.00    0.00  
Теперь ваш сервер находится по адресу 2.tcp.ngrok.io на порту 17018.  
Поздравляю! У вас всё получилось!