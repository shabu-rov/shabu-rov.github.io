# Управление Rooky через RRStudio на Windows
## Подготовка

1. Выполнить [подготовку Windows](/WSL2/preparing_windows)
2. Потребуется скачать ROS Kinetic ~2Gb:
   * Нажать **Win + X**
   * Выбрать окно **PowerShell (админ)**
   * Подать следующие команды:
     ```PowerShell
     wsl
     sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
     sudo apt install curl # Если curl не установлен
     curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
     sudo apt-get update
     sudo apt-get install ros-kinetic-desktop-full
     sudo apt install python-rosdep
     sudo rosdep init
     rosdep update
     echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
     source ~/.bashrc
     ```
   * Установить пакет с серверным ПО **promobot-edu-control**
     * Добавить в систему ppa репозиторий (если не добавлен)
       ```sh
       curl -s --compressed "https://Promobot-education.github.io/ppa/KEY.gpg" | sudo apt-key add -
       sudo curl -s -o /etc/apt/sources.list.d/promobot-education.list "https://Promobot-education.github.io/ppa/promobot-education.list"
       ```
     * Установить пакет:
       ```sh
       sudo apt update
       sudo apt install promobot-edu-control
       ```
     * Добавить путь до файлов серверного ПО
       ```sh
       echo "source /opt/promobot/EduControl/install/setup.bash" >> ~/.bashrc
       source ~/.bashrc
       ```
     * Проверить зависимости
       ```sh
       cd /opt/promobot/EduControl
       rosdep install --from-paths install --ignore-src -r -y
       ```

## Запуск для работы с реальным устройством
  
<details style="margin: 10px 0px 10px 10px;">
	<summary style="color:#069;">Правильный запуск WSL</summary>
	<div style="margin-top: 20px;">
    <p>ℹ️ Если не настраивали текущий COM порт - <a href="/WSL2/com_setup">настроить</a></p>
    <p>ℹ️ Для корректной работы с реальным устройством, подключенным по USB необходимо всегда запускать две утилиты:</p>
    <ol>
      <li>На стороне <strong>Windows</strong> запустить сервер:
        <ul>
          <li>нажать <strong>Win + X</strong></li>
          <li>выбрать <strong>PowerShell (админ)</strong></li>
          <li>подать команду:
            <pre><code class="language-PowerShell">python.exe 'C:\Program Files (x86)\Promobot\WSL2-main\utils\Server.py'</code></pre>
            <blockquote>
              <p>Если происходит ошибка на этапе import serial, необходимо подать команду в PowerShell:</p>
              <pre><code class="language-PowerShell">pip install pyserial</code></pre>
            </blockquote>
          </li>
          <li>свернуть окно PowerShell</li>
        </ul>
      </li>
      <li>На стороне <strong>Linux</strong> запустить клиент (в <strong>новом</strong> окне PowerShell)
        <ul>
          <li>запустить WSL командой:
            <pre><code class="language-PowerShell">wsl</code></pre>
          </li>
          <li>подать команду:
            <div class="language-sh highlighter-rouge">
              <div class="highlight">
                <pre class="highlight"><code><span class="nb">sudo </span>socat <span class="nt">-d</span> <span class="nt">-d</span> pty,link<span class="o">=</span>/dev/RS_485,raw,echo<span class="o">=</span>0,perm<span class="o">=</span>0666 tcp:<span class="nv">$HOST_ADDR</span>:5000</code></pre>
              </div>
            </div>
          </li>
        </ul>
      </li>
      <li>Оба запущенных PowerShell можно <strong>свернуть</strong>, чтобы не мешались.</li>
    </ol>
    <p>ℹ️ Не стоит забывать про <a href="/WSL2/preparing_windows#запуск-x-сервера">X-сервер</a>, он всегда должен быть запущен.</p>
    <p><img src="/WSL2/res/tray.png" alt="tray"></p>
  </div>
</details>

***
**Далее:**
* Запустить **новое** окно PowerShell:
  * нажать **Win + X**
  * выбрать **PowerShell (админ)**
* Запустить Linux командой:
   ```PowerShell
   wsl
   ```
* В зависимости от типа Rooky запустить ROS командой:
  * **Для левой Rooky:**
    ```sh
    roslaunch promobot_control promobot_hardware.launch side:=left
    ```
  * **Для правой Rooky:**
    ```sh
    roslaunch promobot_control promobot_hardware.launch side:=right
    ```
* Запустить [RRStudio в Windows](/RRStudio/setup_windows)
* Выбрать в RRStudio соответствующее устройство.

## Запуск для работы в режиме симуляции, без реального устройства
Запуск симуляции происходит аналогично запуску с реальным устройством.  
Отличаются только команды на запуск серверного ПО (ROS):  
* **Для левой Rooky:**
  ```sh
  roslaunch promobot_control start_simulation.launch side:=left
  ```
* **Для правой Rooky:**
  ```sh
  roslaunch promobot_control start_simulation.launch side:=right
  ```