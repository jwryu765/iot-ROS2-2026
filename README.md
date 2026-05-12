# iot-ROS2-2026
IoT개발자 과정 ROS 로봇 프로그래밍

## 1일차
- 다운로드 및 세팅

- 라즈베리파이에 다운로드
    - 라즈베리 이메저를 통해 라즈베리파이 SD카드 초기화 및 재설치(우분투설치)
    - 가상모니터 VNC를 사용하기 위해 아래처럼 세팅
        ```text
        rpi@rospi
        1.  ip a
        2.  sudo apt update
        3.  sudo apt upgrade
        4.  ip a
        5.  ls
        6.  cd downloads
        7.  cd Downloads/
        8.  wget https://downloads.realvnc.com/file/vnc.files/VNC-server-7.16.0-Linux-ARM64.deb
        9.  wget https://downloads.realvnc.com/file/vnc.files/VNC-Server-7.16.0-Linux-ARM64.deb
        10.  wget https://downloads.realvnc.com/download/file/vnc.files/VNC-Server-7.16.0-Linux-ARM64.deb
        11.  ls
        12.  chmod u+x VNC-Server-7.16.0-Linux-ARM64.deb
        13.  sudo apt install ./VNC-Server-7.16.0-Linux-ARM64.deb
        14.  ls
        15.  sudo apt install
        16.  sudo apt install ./VNC-Server-7.16.0-Linux-ARM64.deb
        17.  clear
        18.  sudo nano /etc/nanorc
        19.  sudo nano /etc/gdm3/custom.conf
        20.  sudo apt install xserver-xorg-video-dummy xinit
        21.  ls /etc
        22.  cd ..

        23.  sudo nano /etc/X11/xorg.conf
            Section "Device"
                Identifier "Configured Video Device"
                Driver "dummy"
            EndSection
            
            Section "Monitor"
                Identifier "Configured Monitor"
                HorizSync 28-80
                VertRefresh 48-75
                Modeline "1920x1080" 172.80 1920 2040 2248 2576 1080 1081 1084 1118
            EndSection

            Section "Screen"
                Identifier "Default Screen"
                Device "Configured Video Device"
                Monitor "Configured Monitor"
                DefaultDepth 24
                SubSection "Display"
                        Depth 24
                        Modes "1920x1080"
                EndSubSection
            EndSection

        24.  sudo systemctl enable vncserver-x11-serviced.service
        25.  sudo systemctl start vncserver-x11-serviced.service
        26.  sudo systemctl status vncserver-x11-serviced.service

        27.  sudo nano /boot/firmware/config.txt
            hdmi_force_hotplug=1
            59 hdmi_group=2
            60 hdmi_mode=82

        28.  sudo reboot
        29.  sudo systemctl restart gdm3
        ```

## 2일차
- 우분투를 통한 ROS2 프로그래밍
- 기본 기능 써보기(TutleSim)
    ```text
    ros2 run turtlesim turtlesim_node  // 거북이 켜기
    ros2 run turtlesim turtle_teleop_key  // 거북이를 방향키로 움직일수있는 코드
    ```
- jupyter사용
    ```text
    1. sudo apt install python3.12-venv
       python3 -m venv --system-site-packages .venv
       source .venv/bin/activate
       python -m pip install --upgrade pip
       python -m pip install ipykernel
       pip3 install jupyter lab
       jupyter lab

    2. jupyter server --generate-config
       nano ~/.jupyter/jupyter_server_config.py

       파일 맨아래로 가서 다음과 같은 내용 추가
       c.ServerApp.ip = '0.0.0.0'
       c.ServerApp.port = 7890
       c.ServerApp.port_retries = 0
       c.ServerApp.open_browser = False

    3. python -m ipykernel install --user --name .venv --display-name "python(ros:jazzy)"
       ```
