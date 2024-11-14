# ЛР №1
#### Чумаченко Александр А-07-22
<br><br>



<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 1</p>

---

#### 1. Проверьте, что каталог lab_work существует и содержит файлы и каталоги, указанные в заданиях.
```
ls -l ~/lab_work
```
```
astravmuser@astravm-23-28:~$ ls -l ~/lab_work/
итого 12
-rw-r--r-- 1 astravmuser astravmuser 14 сен  8 18:21 file1.txt
-rw-r--r-- 1 astravmuser astravmuser 14 сен  8 18:21 file2.txt
-rw-r--r-- 1 astravmuser astravmuser 30 сен  8 18:21 file3.txt
```
---
#### 2. Убедитесь, что все файлы созданы и содержат ожидаемое содержимое.
```
cat ~/lab_work/subdir/file1.txt
cat ~/lab_work/subdir/file2.txt
cat ~/lab_work/file3.txt
cat ~/lab_work/file4.txt
cat ~/lab_work/subdir/file5.txt
cat ~/lab_work/file6.txt
```

> file1.txt file2.txt file3.txt file4.txt file5.txt
```
astravmuser@astravm-23-28:~/lab_work$ cat ~/lab_work/subdir/file1.txt
This is file1
astravmuser@astravm-23-28:~/lab_work$ cat ~/lab_work/subdir/file2.txt
This is file2
astravmuser@astravm-23-28:~/lab_work$ cat ~/lab_work/file3.txt
This is updated_file3.txt
Bla Bla Bla
This is additional line.
astravmuser@astravm-23-28:~/lab_work$ cat ~/lab_work/file4.txt
file1.txt
file2.txt
astravmuser@astravm-23-28:~/lab_work$ cat ~/lab_work/subdir/file5.txt
This is updated_file3.txt
Bla Bla Bla
This is additional line.
```

> В файле file6.txt - помощь по команде ls, полный вывод можно посмотреть при демонстрации

![alt text](image-3.png)


---


#### 3. Содержимое до удаления каталога subdir и после удаления файла file5.txt

```
astravmuser@astravm-23-28:~/lab_work$ ls -l ~/lab_work/subdir/
итого 8
-rw-r--r-- 1 astravmuser astravmuser 14 сен  8 18:21 file1.txt
-rw-r--r-- 1 astravmuser astravmuser 14 сен  8 18:21 file2.txt
```

---

#### 4. Удаление каталога subdir

```
astravmuser@astravm-23-28:~/lab_work$ rm -r subdir
astravmuser@astravm-23-28:~/lab_work$ ls
file3.txt  file6.txt
```

---

#### 5. Удаление file3.txt и find

```
astravmuser@astravm-23-28:~/lab_work$ rm file3.txt
astravmuser@astravm-23-28:~/lab_work$ find ~/lab_work -name "file2.txt"
astravmuser@astravm-23-28:~/lab_work$ find ~/lab_work -type f -name  "*.txt"     
/home/astravmuser/lab_work/file6.txt
```

---

#### 6. grep "ls" file6.txt

![alt text](image-7.png)

> Полный вывод можно посмотреть при демонстрации

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 2</p>

---

#### 1. Команды ls *.txt, ls file?.txt, и ls file{1,2,3}.txt должны корректно отображать соответствующие файлы.

```
astravmuser@astravm-23-28:~/part2$ ls *.txt
file1.txt  file2.txt  file3.txt  fileA.txt  fileB.txt
astravmuser@astravm-23-28:~/part2$ ls file?.txt
file1.txt  file2.txt  file3.txt  fileA.txt  fileB.txt
astravmuser@astravm-23-28:~/part2$ ls file{1,2,3}.txt   
file1.txt  file2.txt  file3.txt
```

---

#### 2. Строки с одинарными кавычками ('file?.txt') и двойными кавычками ("$myvar") должны выводиться корректно.

```
astravmuser@astravm-23-28:~/part2$ echo 'file?.txt'
file?.txt
astravmuser@astravm-23-28:~/part2$ echo "$myvar"
file*.txt
```

---

#### 3. Файл file with spaces.txt должен содержать текст "This is a test file with spaces.".

```
astravmuser@astravm-23-28:~/part2$ cat "file with spaces.txt"                               
This is a test file with spaces.
```

---

#### 4. Файл numbers.txt должен содержать числа от 1 до 10, строку "Additional text", и замену 1 на ONE.

```
astravmuser@astravm-23-28:~/part2$ echo "1, 2, 3, 4, 5, 6, 7, 8, 9, 10" > numbers.txt
astravmuser@astravm-23-28:~/part2$ cat numbers.txt
1, 2, 3, 4, 5, 6, 7, 8, 9, 10
astravmuser@astravm-23-28:~/part2$ echo "Additional text" >> numbers.txt
astravmuser@astravm-23-28:~/part2$ cat numbers.txt                       
1, 2, 3, 4, 5, 6, 7, 8, 9, 10
Additional text
astravmuser@astravm-23-28:~/part2$ sed -i 's/1/ONE/g' numbers.txt  astravmuser@astravm-23-28:~/part2$ cat numbers.txt                 
ONE, 2, 3, 4, 5, 6, 7, 8, 9, ONE0
Additional text
```

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 3</p>

---

#### 1. Скрипт script1.sh: 
- Выводит "Hello, world!" при запуске.

```
astravmuser@astravm-23-28:~/part3$ nano script1.sh
astravmuser@astravm-23-28:~/part3$ chmod +x script1.sh  
astravmuser@astravm-23-28:~/part3$ ./script1.sh  Hello, world!
```

---

#### 2. Скрипт script2.sh:
- Корректно принимает и выводит параметр при запуске (например, "Hello, Alice!").

```
astravmuser@astravm-23-28:~/part3$ nano script2.sh
astravmuser@astravm-23-28:~/part3$ chmod +x script2.sh
astravmuser@astravm-23-28:~/part3$ ./script2.sh Alice
Hello, Alice!
```

- Отображает сообщение о неверном использовании, если параметр не передан.

```
astravmuser@astravm-23-28:~/part3$ ./script2.sh
Usage: ./script2.sh <name>
```

---

#### 3. Скрипт script3.sh:
- Корректно выводит количество строк и слов для существующего файла.

```
astravmuser@astravm-23-28:~/part3$ nano script3.sh
astravmuser@astravm-23-28:~/part3$ chmod +x script3.sh   
astravmuser@astravm-23-28:~/part3$ echo -e "Line 1\nLine 2\nLine 3" > testfile.txt
astravmuser@astravm-23-28:~/part3$ ./script3.sh testfile.txt  File: testfile.txt
Lines: 3
Words: 6
```

- Выводит сообщение о несуществующем файле, если файл не найден.

```
astravmuser@astravm-23-28:~/part3$ ./script3.sh testfle.txt   
File testfle.txt does not exist.
astravmuser@astravm-23-28:~/part3$ ./script3.sh
Usage: ./script3.sh <filename>
```

---

#### 4. Скрипт script4.sh:
- Корректно обрабатывает и выводит информацию о текстовых файлах в текущем каталоге.

```
astravmuser@astravm-23-28:~/part3$ nano script4.sh
astravmuser@astravm-23-28:~/part3$ chmod +x script4.sh  
astravmuser@astravm-23-28:~/part3$ echo "Sample text" > file1.txt
astravmuser@astravm-23-28:~/part3$ echo "Another sample text" > file2.txt
astravmuser@astravm-23-28:~/part3$ ls
file1.txt  file2.txt  script1.sh  script2.sh  script3.sh  script4.sh  testfile.txt
astravmuser@astravm-23-28:~/part3$ ./script4.sh  
Processing file: file1.txt
Lines in file1.txt: 1
Processing file: file2.txt
Lines in file2.txt: 1
Processing file: testfile.txt
Lines in testfile.txt: 3
astravmuser@astravm-23-28:~/part3$ echo "Additional line" >> file2.txt  
astravmuser@astravm-23-28:~/part3$ ./script4.sh                         
Processing file: file1.txt
Lines in file1.txt: 1
Processing file: file2.txt
Lines in file2.txt: 2
Processing file: testfile.txt
Lines in testfile.txt: 3
```

- Выводит сообщение, если текстовые файлы не найдены.

```
astravmuser@astravm-23-28:~/part3$ cd ..
astravmuser@astravm-23-28:~$ ls
Desktop  Desktops  lab_work  part2  part3  SystemWallpapers  Видео  Документы  Загрузки  Изображения  Музыка  Общедоступные  Шаблоны
astravmuser@astravm-23-28:~$ cd part3
astravmuser@astravm-23-28:~/part3$ mv script4.sh ../
astravmuser@astravm-23-28:~/part3$ cd ..
astravmuser@astravm-23-28:~$ ./script4.sh  
No text files found.
```

---


#### 5.	Установка Ansible:
- Ansible установлен и версия проверена.

```
astravmuser@astravm-23-28:~$ ansible --version
ansible 2.7.7
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/astravmuser/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.7.3 (default, Sep 19 2023, 08:52:39) [GCC 8.3.0]
```

---

#### 6.	Настройка инвентарного файла:
- Файл inventory корректно настроен и распознается Ansible.

```
astravmuser@astravm-23-28:~$ nano inventory
astravmuser@astravm-23-28:~$ mv inventory ./part3
astravmuser@astravm-23-28:~$ cd part3
astravmuser@astravm-23-28:~/part3$ ls
file1.txt  file2.txt  inventory  script1.sh  script2.sh  script3.sh  testfile.txt
astravmuser@astravm-23-28:~/part3$ cat inventory  
[local]
localhost ansible_connection=local

astravmuser@astravm-23-28:~/part3$ ansible-inventory --list -i inventory  
{
    "_meta": {
        "hostvars": {
            "localhost": {
                "ansible_connection": "local"
            }
        }
    },
    "all": {
        "children": [
            "local",
            "ungrouped"
        ]
    },
    "local": {
        "hosts": [
            "localhost"
        ]
    },
    "ungrouped": {}
}
```

---

#### 7.	Простой плейбук:
- Плейбук playbook.yml успешно устанавливает пакет apache2.

```
astravmuser@astravm-23-28:~/part3$ nano playbook.yml
astravmuser@astravm-23-28:~/part3$ cat playbook.yml  
---
- name: Ensure Apache is installed
  hosts: local
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present

astravmuser@astravm-23-28:~/part3$ ansible-playbook -i inventory playbook.yml  

PLAY [Ensure Apache is installed] **********************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************
ok: [localhost]

TASK [Install Apache] ******************************************************************************************************************************************************************
changed: [localhost]

PLAY RECAP *****************************************************************************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```

```
astravmuser@astravm-23-28:~/part3$ dpkg -l | grep apache2
ii  apache2                                       2.4.57-2+astra.se2                                     amd64        Apache HTTP Server
ii  apache2-bin                                   2.4.57-2+astra.se2                                     amd64        Apache HTTP Server (modules and other binary files)
ii  apache2-data                                  2.4.57-2+astra.se2                                     all          Apache HTTP Server (common files)
ii  apache2-utils                                 2.4.57-2+astra.se2                                     amd64        Apache HTTP Server (utility programs for web servers)
```

---

#### 8.	Использование ролей:
- Роль myrole корректно применяется и выполняет установку и запуск Apache.

```
astravmuser@astravm-23-28:~/part3$ ansible-galaxy init myrole
- myrole was created successfully
astravmuser@astravm-23-28:~/part3$ cat playbook.yml >> myrole/tasks/main.yml  astravmuser@astravm-23-28:~/part3$ nano myrole/tasks/main.yml                 
astravmuser@astravm-23-28:~/part3$ nano playbook_with_role.yml
astravmuser@astravm-23-28:~/part3$ ansible-playbook -i inventory playbook_with_role.yml


PLAY [Apply myrole] ************************************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************
ok: [localhost]

TASK [myrole : Ensure Apache is installed] *********************************************************************************************************************************************
ok: [localhost]

TASK [myrole : Start Apache service] ***************************************************************************************************************************************************
ok: [localhost]

PLAY RECAP *****************************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0
```

```
astravmuser@astravm-23-28:~/part3$ systemctl status apache2
● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2024-09-20 00:50:22 MSK; 8min ago
     Docs: https://httpd.apache.org/docs/2.4/
 Main PID: 28230 (apache2)
    Tasks: 6 (limit: 4915)
   Memory: 6.7M
      CPU: 54ms
   CGroup: /system.slice/apache2.service
           ├─28230 /usr/sbin/apache2 -k start
           ├─28232 /usr/sbin/apache2 -k start
           ├─28233 /usr/sbin/apache2 -k start
           ├─28234 /usr/sbin/apache2 -k start
           ├─28235 /usr/sbin/apache2 -k start
           └─28236 /usr/sbin/apache2 -k start
```

---

#### 9.	Файлы и шаблоны:
- Шаблон hello.conf.j2 успешно используется для создания конфигурационного файла /etc/hello.conf с правильным содержимым.

```
astravmuser@astravm-23-28:~/part3$ nano myrole/templates/hello.conf.j2
astravmuser@astravm-23-28:~/part3$ nano myrole/tasks/main.yml                           
astravmuser@astravm-23-28:~/part3$ nano playbook_with_role.yml                                                                              astravmuser@astravm-23-28:~/part3$ ansible-playbook -i inventory playbook_with_role.yml
 [WARNING]: Found variable using reserved name: name


PLAY [Apply myrole] ************************************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************
ok: [localhost]

TASK [myrole : Ensure Apache is installed] *********************************************************************************************************************************************
ok: [localhost]

TASK [myrole : Start Apache service] ***************************************************************************************************************************************************
ok: [localhost]

TASK [myrole : Create configuration file from template] ********************************************************************************************************************************
changed: [localhost]

PLAY RECAP *****************************************************************************************************************************************************************************
localhost                  : ok=4    changed=1    unreachable=0    failed=0    

astravmuser@astravm-23-28:~/part3$ cat /etc/hello.conf  
ini
Copy code
[settings]
greeting = Hello World!
```

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 4</p>

---

#### 1.	Управление процессами:
- Процесс может быть успешно приостановлен, возобновлен и завершен с помощью команд kill и соответствующих сигналов.

```
astravmuser@astravm-23-28:~/part4$ sleep 600 &
[3] 32072
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32072  0.0  0.0   5260   748 pts/0    S    01:11   0:00 sleep 600
astravm+ 32075  0.0  0.0   6092   884 pts/0    R+   01:11   0:00 grep sleep
astravmuser@astravm-23-28:~/part4$ kill -SIGSTOP 32072
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32072  0.0  0.0   5260   748 pts/0    T    01:11   0:00 sleep 600
astravm+ 32078  0.0  0.0   6092   880 pts/0    S+   01:12   0:00 grep sleep
[3]+  Остановлен    sleep 600
astravmuser@astravm-23-28:~/part4$ kill -SIGCONT 32072
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32072  0.0  0.0   5260   748 pts/0    S    01:11   0:00 sleep 600
astravm+ 32083  0.0  0.0   6092   816 pts/0    S+   01:12   0:00 grep sleep
astravmuser@astravm-23-28:~/part4$ kill -SIGTERM 32072
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32087  0.0  0.0   6092   884 pts/0    S+   01:12   0:00 grep sleep
[3]   Завершено      sleep 600
astravmuser@astravm-23-28:~/part4$ kill -SIGKILL 32072
bash: kill: (32072) - Нет такого процесса
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32089  0.0  0.0   6092   876 pts/0    S+   01:13   0:00 grep sleep
```

---

#### 2.	Изменение приоритета процессов:
- Команды nice и renice корректно устанавливают и изменяют приоритет процессов.

```
astravmuser@astravm-23-28:~/part4$ nice -n 10 sleep 600 &
[3] 32103
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep    
astravm+ 32103  0.0  0.0   5260   688 pts/0    SN   01:13   0:00 sleep 600
astravm+ 32109  0.0  0.0   6092   876 pts/0    S+   01:13   0:00 grep sleep
astravmuser@astravm-23-28:~/part4$ sudo renice -n -10 -p 32103
32103 (process ID) old priority 10, new priority -10
astravmuser@astravm-23-28:~/part4$ kill -SIGKILL 32103
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep         
astravm+ 32120  0.0  0.0   6092   884 pts/0    S+   01:15   0:00 grep sleep
[3]   Убито              nice -n 10 sleep 600
astravmuser@astravm-23-28:~/part4$ ps aux | grep sleep
astravm+ 32122  0.0  0.0   6092   884 pts/0    S+   01:15   0:00 grep sleep
```

---

#### 3.	Работа с фоновыми задачами:
- Команды jobs, fg, и bg правильно управляют фоновыми задачами и их состоянием.

> лютый ужас в консоли от google, сюда вставлять не буду все
> можно решить перенаправлением в файл, ping google.com > ping_output_file.txt & но опять же там будет много строк

```
stravmuser@astravm-23-28:~/part4$ ping google.com &
[3] 32126
astravmuser@astravm-23-28:~/part4$ PING google.com (142.250.185.206) 56(84) bytes of data.
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=1 ttl=112 time=62.2 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=2 ttl=112 time=113 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=3 ttl=112 time=45.2 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=4 ttl=112 time=44.7 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=5 ttl=112 time=44.5 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=6 ttl=112 time=45.2 ms
64 bytes from fra16s52-in-f14.1e100.net (142.250.185.206): icmp_seq=7 ttl=112 time=46.1 ms
```

```
astravmuser@astravm-23-28:~/part4$ jobs
[1]-  Остановлен    nano script2.sh  (рабочий каталог: ~/part3)
[2]+  Остановлен    nano script3.sh  (рабочий каталог: ~/part3)
[3]   Запущен          ping google.com &
```

```
astravmuser@astravm-23-28:~/part4$ bg %3
bash: bg: задание 3 уже выполняется в фоновом режиме
```

```
astravmuser@astravm-23-28:~/part4$ fg %3
ping google.com
^Z
[3]+  Остановлен    ping google.com
```

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 5</p>

---

####  Создание и управление системным юнитом:
- Созданный сервис работает, его можно запустить, остановить, включить при старте системы и удалить.

```
astravmuser@astravm-23-28:~/part5$ sudo nano /etc/systemd/system/mytest.service
astravmuser@astravm-23-28:~/part5$ sudo systemctl daemon-reload  
astravmuser@astravm-23-28:~/part5$ sudo systemctl start mytest
astravmuser@astravm-23-28:~/part5$ systemctl status mytest
● mytest.service - My Test Service
   Loaded: loaded (/etc/systemd/system/mytest.service; disabled; vendor preset: enabled)
   Active: active (running) since Fri 2024-09-20 02:23:03 MSK; 21s ago
 Main PID: 2074 (bash)
    Tasks: 2 (limit: 4915)
   Memory: 532.0K
      CPU: 3ms
   CGroup: /system.slice/mytest.service
           ├─2074 /bin/bash -c while true; do echo 'Service is running'; sleep 60; done
           └─2079 sleep 60
astravmuser@astravm-23-28:~/part5$ sudo systemctl enable mytest
Created symlink /etc/systemd/system/multi-user.target.wants/mytest.service → /etc/systemd/system/mytest.service.
astravmuser@astravm-23-28:~/part5$ sudo systemctl stop mytest
astravmuser@astravm-23-28:~/part5$ systemctl status mytest      ● mytest.service - My Test Service
   Loaded: loaded (/etc/systemd/system/mytest.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Fri 2024-09-20 02:24:22 MSK; 3s ago
 Main PID: 2074 (code=killed, signal=TERM)
      CPU: 4ms
astravmuser@astravm-23-28:~/part5$ sudo systemctl disable mytest
Removed /etc/systemd/system/multi-user.target.wants/mytest.service.
astravmuser@astravm-23-28:~/part5$ sudo rm /etc/systemd/system/mytest.service  
astravmuser@astravm-23-28:~/part5$ sudo systemctl daemon-reload
astravmuser@astravm-23-28:~/part5$ systemctl status mytest                        
Unit mytest.service could not be found.
```

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 6</p>

---

#### Правильно настроены и выполнены задачи по расписанию, указанные в crontab.
- Скрипты создаются и выполняются согласно заданному расписанию.

```
astravmuser@astravm-23-28:~/part6$ sudo crontab -l                            # Edit this file to introduce tasks to be run by cron.
#  
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#  # To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
#  
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#  # Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#  
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#  # For more information see the manual pages of crontab(5) and cron(8)
#  
# m h  dom mon dow   command

* * * * * /home/youruser/scripts/test_script.sh
0 0 * * * /home/youruser/scripts/daily_script.sh
30 3 * * 1 /home/youruser/scripts/weekly_scripts.sh
0 12 1 * * /home/youruser/scripts/monthly_script.sh


astravmuser@astravm-23-28:~/part6$ ls /home/youruser/scripts/                          daily_script.sh  monthly_script.sh  test_script.sh  weekly_script.sh
```

```
astravmuser@astravm-23-28:~/part6$ sudo cat /home/youruser/cron_test.log      Cron test script executed at Пт сен 20 02:44:01 MSK 2024
Cron test script executed at Пт сен 20 02:45:01 MSK 2024
Cron test script executed at Пт сен 20 02:46:01 MSK 2024
Cron test script executed at Пт сен 20 02:47:01 MSK 2024
Cron test script executed at Пт сен 20 02:48:01 MSK 2024
Cron test script executed at Пт сен 20 02:49:01 MSK 2024
Cron test script executed at Пт сен 20 02:50:01 MSK 2024
Cron test script executed at Пт сен 20 02:51:01 MSK 2024
Cron test script executed at Пт сен 20 02:52:01 MSK 2024
```

> ждать месяц, чтобы проверить работы скриптов не хочется, поэтому можно просто показать содержимое файлов

---

<br><br><br><br><br><br>

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 7</p>

---

#### 1.	Установка и настройка QEMU/KVM:
- Пакеты установлены корректно и KVM поддерживается оборудованием.

---

#### 2.	Создание и управление виртуальными машинами через virt-manager:
- Виртуальная машина создана и успешно запущена через графический интерфейс.

---

#### 3.	Управление виртуальными машинами с помощью virsh:
- Команды virsh используются для создания, запуска, остановки и удаления виртуальных машин.

---

#### 4.	Работа с образами и конфигурацией:
- Создание и добавление новых дисков, а также управление конфигурацией виртуальной машины выполнены успешно.

---







