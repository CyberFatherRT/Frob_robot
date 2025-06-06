<div align="center" style="text-align: center;">

# Роботизированная платформа Frob

![Логотип Frob](https://via.placeholder.com/150)

[English documentation](./README.md)

**Frob** - это недорогой мобильный робот с открытым исходным кодом, созданный для популяризации робототехники и обучения [ROS](https://www.ros.org/). Он предназначен для энтузиастов, студентов и преподавателей, изучающих мир робототехники. Независимо от того, являетесь ли вы начинающим или опытным разработчиком, Frob предоставляет универсальную платформу для решения широкого спектра задач обучения.

[![Wiki](https://img.shields.io/badge/Wiki-Documentation-blue?style=flat-square&logo=github)](https://github.com/dark516/Frob_robot/wiki)
[![Telegram](https://img.shields.io/badge/Telegram-Community-blue?style=flat-square&logo=telegram)](https://t.me/FrobCommunity)
[![License](https://img.shields.io/github/license/dark516/Frob_robot?style=flat-square)](https://github.com/dark516/Frob_robot/blob/main/LICENSE)
[![Issues](https://img.shields.io/github/issues/dark516/Frob_robot?style=flat-square)](https://github.com/dark516/Frob_robot/issues)

---
</div>

## Оглавление
- [Установка](#Установка-и-конфигурация)
- [Изготовление и сборка](#Изготовление-и-сборка)
- [Основное использование](#Основное-использование)
- [Задания для выполнения](#Задания-для-выполнения)
- [Рекомендации по внесению вклада](#Рекомендации-по-внесению-вклада)
- [Сообщество](#Сообщество)
- [Лицензия](#Лицензия)

---

## Установка и конфигурация
Чтобы начать работу с этим проектом, выполните следующие действия.
### 1. Клонируйте репозиторий
Начните с клонирования этого репозитория на свой локальный компьютер:
```bash
git clone https://github.com/dark516/Frob_robot
cd Frob_robot
```

### 2. Установите ROS2
Для этого проекта требуется ROS2 (мы рекомендуем использовать ROS-Jazzy). Существует два варианта установки ROS2-jazzy:
#### Вариант А: Установите ROS2, используя предоставленные скрипты
В каталоге [installation](./установка) вы найдете скрипты для установки ROS2 Jazzy вместе с необходимыми зависимостями для разных компьютеров. Чтобы использовать скрипты, выполните одну из следующих команд, в зависимости от устройства, на которое вы устанавливаете.:
##### Установите ROS2 на рабочую станцию (ноутбук или ПК)
```bash
bash ./installation/install_jazzy_full.sh
```
##### Установите ROS2 на Raspberry pi (робот)
```bash
bash ./installation/install_jazzy_base.sh
```
#### Вариант B: Ручная установка ROS2
Если вы предпочитаете установить ROS2 вручную, пожалуйста, ознакомьтесь с официальным руководством по установке ROS2 [здесь](https://docs.ros.org/en/jazzy/Installation.html). В этом руководстве приведены пошаговые инструкции по настройке ROS2 Jazzy на различных платформах.

## Изготовление и сборка
<!-- Предоставьте подробные инструкции по изготовлению и сборке робота. -->
<!-- Включите информацию о 3D-печати, необходимых материалах и пошаговом руководстве по сборке. -->
## Основное использование
### Подключение к роботу
Для подключения к роботу можно использовать команду
```bash
ssh robot@r1.frob-robot.online
```
Заменив r1 на id вашей платформы. Или воспользоваться классическим методом подключения через ip адрес. Вы можете посмотреть IP на раздающем сеть устройстве или установить плагин для сканирования всех IP-адресов:
```bash
sudo apt install arp-scan
```
И запустить сканирование:
```bash
sudo arp-scan --localnet
```
![Пример arp-scan с выделенными IP-адресами](https://github.com/dark516/Frob_robot/blob/main/images/arp-scan.jpg?raw=true)
После определения IP-адреса, подключитесь к роботу через SSH:
```bash
ssh robot@ip
```
![Пример подключения по ssh](https://github.com/dark516/Frob_robot/blob/main/images/ssh.jpg?raw=true)
### Рабочая директория
Рабочая директория содержит весь исходный код проекта и служит для его сборки и настройки. Для перехода в неё выполните:
```bash
cd ros2/src/ros2_ws/
```
Для использования робота требуется собрать все пакеты
```bash
colcon build
source install/setup.bash
```
### Запуск робота
Для запуска большинства функциональных модулей выполните в рабочей директории на роботе:
```bash
ros2 launch frob_bringup bringup.launch.py
```
После запуска всех пакетов через launch-файл можно проверять отдельные компоненты.
#### Проверка движений
ros2_arduino_bridge — пакет для связи с низкоуровневым контроллером робота (Arduino), запущенный с помощью launch-файла. Пакет позволяет отправлять команды на контроллер и получать данные от него, включая управление моторами.

Для проверки движений откройте новый терминал на компьютере и запустите графический джойстик управления роботом:
```bash
rqt
```
И запустите «Plugins» → «Robot Tools» → «Robot Steering».
![Интерфейс RQT](https://github.com/dark516/Frob_robot/blob/main/images/rqt.jpg?raw=true)

Плагин Robot Steering из пакета rqt позволяет управлять движением робота через графический интерфейс, отправляя команды на контроллер (Arduino) через ROS 2.
Использование плагина «Robot Steering»

Настройка управления:

- Убедитесь, что в поле Topic указан правильный топик для управления роботом (например, /cmd_vel).
Топик должен совпадать с настройками в пакете ros2_arduino_bridge.

- Настройте параметры (например, линейную и угловую скорость) с помощью ползунков в интерфейсе.

Проверка движения:

- Используйте ползунки или вводите значения в поля для управления скоростью и направлением.

- Проверьте, что робот корректно реагирует на команды, отправляемые из интерфейса.

Отладка

Если робот не реагирует:

-	Проверьте, работает ли запуск ros2_arduino_bridge.

-	Убедитесь, что при закрытом rqt указанный топик (/cmd_vel) создан на вашем компьютере
-	Обратитесь к разделу [Решение ошибок](#Решение-ошибок)
```bash
ros2 topic list
```

-	Проверьте соединение Arduino и параметры моторов.

#### Визуализация перемещений (одометрии)
Вы можете визуализировать движение робота с помощью пакета одометрии (frob_odometry). Для этого выполните:
```bash
ros2 launch frob_description display_odom.launch.py
```
Теперь при движении колес перемещение робота будет отображаться на экране
#### Запуск камеры

##Задания для выполнения

## Решение ошибок
### Отсутствие топиков
Если после создания топиков они не видны на роботе или компьютере, выполните следующие шаги. Проверьте список топиков командой:
```bash
ros2 topic list
```
Сравните вывод на роботе и компьютере — он должен совпадать.
Инструкции ниже приведены в порядке важности. После выполнения каждого шага повторно проверьте список топиков.

#### 1. Перезагрузка систем
Перезагрузите робота и компьютер. Это часто решает проблему:
```bash
sudo reboot now
```
#### 2. Проверка ROS_DOMAIN_ID
Убедитесь, что переменная ```ROS_DOMAIN_ID``` совпадает на роботе и компьютере:
```bash
echo $ROS_DOMAIN_ID
```
Если значения различаются, задайте одинаковое значение в файле ```~/.bashrc```:
```bash
export ROS_DOMAIN_ID=78
```
Примените изменения:
```bash
source ~/.bashrc
```

#### 3. Выключение фаервола
Фаервол может блокировать передачу сообщений ROS. Отключите его:
```bash
sudo ufw dusable
```
#### 4. Перезагрузка ros daemon
Попробуйте перезапустить ROS Daemon:
```bash
ros2 daemon stop
ros2 daemon start
```

### Проблемы в частях робота
#### Выключается модуль raspberry
Raspberry Pi может выключаться по нескольким причинам:
##### 1. Разряжен аккумулятор
Проверьте уровень заряда аккумулятора. Зарядите его при низком напряжении.
##### 2. Провод питания
Проверьте надежность соединения кабеля. Если кабель поврежден, замените его.
##### 3. Чрезмерные нагрузки
Маломощный преобразователь питания не рассчитан на длительные высокие нагрузки. Для мониторинга нагрузки и температуры процессора установите btop:
```
sudo apt install btop
btop
```
![Интерфейс btop](https://github.com/dark516/Frob_robot/blob/main/images/btop.jpg?raw=true)
Для разовой высокой нагрузки используйте USB-C разъем вместо основного модуля питания, предварительно отключив его
##### 4. Заниженное напряжение
Проверьте напряжение на выходе модуля питания. Оно должно быть в диапазоне 5.0–5.3 В. Настройте его вращением потенциометра на преобразователе.
##### 5. Мощные модули
Отключите устройства с высоким энергопотреблением (моторы, сервоприводы и т.д.). Для таких модулей используйте разъем ```other``` на модуле питания или подключите их к Arduino.
##### 6. Замена Raspberry PI
Если ни один из шагов не помог, возможно, Raspberry Pi неисправна. Рассмотрите замену или ремонт устройства.

#### Некорректная работа Arduino модуля
##### 1. Arduino не прошивается
- Переподключите Arduino к компьютеру.
- Убедитесь, что в программе выбран правильный порт и плата.
- Загрузите пустой скетч.
- Проверьте, чтобы пины модулей были правильно подключены.
- Установите драйвер CH340, если требуется.
- Замените Arduino UNO, если проблема не решена.

##### 2. Некорректная работа моторов
- Загрузите скетч проверки моторов.
- Убедитесь в правильном подключении пинов моторов и энкодеров.
- Проверьте, чтобы пины модулей были в хорошем состоянии.
- Замените неисправный модуль, если требуется.
  

## Рекомендации по внесению вклада
Мы всегда рады инициативе и поддержке сообщества в развитии проекта Frob. Ниже приведён общий порядок действий для внесения вклада, а также информация о том, как сообщать о проблемах и следовать стандартам кодирования.
### Общий процесс

#### 1. Форкните репозиторий
Создайте собственную копию проекта с помощью кнопки Fork на GitHub.
#### 2. Создайте отдельную ветку
Для каждой новой функции или исправления ошибки создайте отдельную ветку:
```
git checkout -b feature/имя_функции
```
#### 3. Реализуйте изменения
Добавьте новые возможности, исправьте баги или обновите документацию. Убедитесь, что ваш код:

- работает корректно

- хорошо структурирован

- сопровождается понятными комментариями и тестами (если необходимо)

#### 4. Протестируйте изменения
Убедитесь, что проект собирается без ошибок и не ломает существующую функциональность:
```
colcon build --packages-select frob_<название_пакета>
```

#### 5. Сделайте commit и push
Добавьте свои изменения в Git с осмысленным сообщением:
```
git commit -m "Добавлена функция автоматического поворота"
git push origin feature/имя_функции
```

#### 6. Создайте Pull Request (PR)
Перейдите в ваш репозиторий на GitHub и нажмите "New Pull Request". В описании укажите, какие изменения вы внесли и зачем.

## Сообщество

Frob - это активно развивающийся проект, и мы искренне приглашаем вас присоединиться к нашему сообществу. Независимо от того, сталкиваетесь ли вы с проблемами или ищете свежие идеи, наше сообщество всегда готово поддержать вас.

- **[Присоединяйтесь к нашему чату сообщества в Telegram](https://t.me/FrobCommunity)**: Общайтесь с другими пользователями Frob, задавайте вопросы, делитесь своим опытом и будьте в курсе последних событий.

Ваше участие может помочь сформировать будущее Frob. Мы с нетерпением ждем ваших идей и вклада!

## Лицензия

На Frob распространяется лицензия [Apache License 2.0](./LICENSE).
Для получения подробного представления о ваших правах и обязанностях, пожалуйста, ознакомьтесь с [полным текстом лицензии](./LICENSE).
