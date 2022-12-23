# jbrowser
# Theory 
0.4] What are computer ports on a high level? How many ports are there on a typical computer?

В компьютерах есть два вида портов — физические и программные (или сетевые):
Физический порт — это разъём на компьютере, с помощью которого можно подключить флешку, сетевой кабель, принтер, наушники и так далее. Физический порт обменивается электричеством с устройством, который вставлен в этот порт.
Сетевой порт — то число, которое записывается в заголовках протоколов транспортного уровня сетевой модели OSI. Оно используется для определения программы или процесса-получателя пакета в пределах одного IP-адреса.Порты позволяют определить сетевые приложения, работающие на компьютере, множество которых может быть запущено одновременно. Основными сетевыми программами могут быть:
WEB-сервер – предоставляет трансляцию данных с веб-сайтов;
Сервер почты – позволяет обмениваться электронными письмами;
FTP-сервер – обеспечивает передачу информации.
Основным предназначением портов является прием и передача данных определенного вида, а также устранение ошибки неоднозначности при попытке установить связь с хостом по IP-адресу. Для обеспечения трансляции данных с веб-сервера необходимо указать IP адрес хоста и номер порта, определяющий программу веб-сервер
Порт отображается в виде 16 битного числа от 1 до 65535. 
Использование портов регламентируется специальной организацией IANA, предоставляющей стандарты при работе с портами.

Когда на определенном хосте пользователь открывает окно браузера и набирает необходимый поисковой запрос, веб-сервер автоматически отправляет пакеты данных по протоколу TCP/IP в порт 80.

В случае использования почтового клиента Outlook Express существуют два стандартизированных порта:

110 порт используется для получения электронных писем;
посредством порта 25 письма отправляются в глобальную сеть в поисках своего адресата.

[0.4] What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.
При отправлении и получении пакетов данных по сети интернет через HTTP используется протокол управления передачей (TCP). Соединение при этом происходит через порт 80. Клиент отправляет запрос на HTTP-сервер, где располагается сайт, после чего сервер посылает ответ. Этот ответ содержит информацию о состоянии завершения. Выглядит это примерно так: HTTP/1.1 200 OK.
HTTPS означает безопасный протокол передачи гипертекста. HTTPS использует порт 443. HTTP работает на уровне приложений, а HTTPS — на транспортном уровне.В HTTP нет шифрования, HTTPS шифрует данные перед отправкой.
Разница между https и ssh
Благодаря ssh можно удаленно подключаться к другой ПК защищенным образом и через оболочку осуществлять манипуляцию операционной системы(защищено) а ssl это протокол который осуществляет безопасную передачу данных(шифрованным образом) то есть создается безопасный канал передачи данных между двумя машинами.

[0.4] Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.

IP-адрес – это уникальный адрес, идентифицирующий устройство в интернете или локальной сети. IP означает «Интернет-протокол» – набор правил, регулирующих формат данных, отправляемых через интернет или локальную сеть.
По сути, IP-адрес – это идентификатор, позволяющий передавать информацию между устройствами в сети: он содержит информацию о местоположении устройства и обеспечивает его доступность для связи. IP-адреса позволяют различать компьютеры, маршрутизаторы и веб-сайты в интернете и являются важным компонентом работы интернета.
Использование IP-адресов обычно происходит незаметно. Процесс работает следующим образом:

Устройство подключается к интернету не напрямую: сначала оно подключается к сети, подключенной к интернету, а сеть, в свою очередь, предоставляет устройству доступ к интернету. Дома, скорее всего, этой сетью является сеть вашего интернет-провайдера. В офисе это будет сеть компании.IP-адрес назначается устройству нашим интернет-провайдером.Интернет-активность проходит через интернет-провайдера, а он перенаправляет ответы на запросы, используя IP-адрес. Поскольку провайдер предоставляет доступ в Интернет, его роль заключается в назначении IP-адрес нашему устройству.В сети Интернет используются именно публичные глобальные адреса(белые). Публичным IP-адресом называется IP-адрес, который используется для выхода в Интернет.

[0.4] What is Nginx? How does it work on the high level? List several alternative web servers.
nginx [engine x] — это HTTP-сервер и обратный прокси-сервер, почтовый прокси-сервер, а также TCP/UDP прокси-сервер общего назначения, изначально написанный Игорем Сысоевым. Уже длительное время он обслуживает серверы многих высоконагруженных российских сайтов, таких как Яндекс, Mail.Ru, ВКонтакте и Рамблер.
Когда пользователь совершает действие на странице, информация передается на сервер. Он находит файлы, передает сведения.

Если обрабатывать запросы каждого пользователя по отдельности, серверу придется одновременно выполнять много процессов. Сайт начнет работать медленно. Nginx позволяет обойти ограничение. Его архитектура асинхронная: все запросы обрабатываются на разных этапах, что повышает скорость обработки.

Запросы от одного пользователя разбиваются на маленькие структуры — сетевые соединения. Обработка происходит быстрее: за однотипные действия отвечает один процесс. После обработки соединения собираются в одном виртуальном контейнере, чтобы преобразоваться в единый первоначальный запрос, а затем отправляются пользователю. Благодаря такому принципу работы Nginx одно сетевое соединение может обслуживать до 1024 запросов.
Альтернативы для nginx
394.
Apache HTTP Server

[0.4] What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.
SSH (Secure Shell — «безопасная оболочка») — это сетевой протокол для удаленного управления операционной системой с помощью командной строки и передачи данных в зашифрованном виде.SSH позволяет безопасно передавать в незащищённой среде практически любой другой сетевой протокол. Таким образом, можно не только удалённо работать на компьютере через командную оболочку, но и передавать по шифрованному каналу звуковой поток или видео (например, с веб-камеры).


# Problem
                   #Загружаем аннотацию и геном

                   wget https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz
                   wget https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
                   
                   #Индексируем все 
                   sudo apt-get install samtools
                   gzip -d Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
                   samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa
                   
                   sudo apt-get install tabix
                   gzip -d Homo_sapiens.GRCh38.108.gff3.gz
                   (grep "^#" Homo_sapiens.GRCh38.108.gff3; grep -v "^#" Homo_sapiens.GRCh38.108.gff3 | sort -t"`printf '\t'`" -k1,1 -k4,4n) | bgzip > Homo_sapiens.GRCh38.108.sort.gff3.gz
                   tabix -p gff Homo_sapiens.GRCh38.108.sort.gff3.gz
                   
                   #bed файлы из домашки
                   wget -O PML.bed.gz 'https://www.encodeproject.org/files/ENCFF480ECN/@@download/ENCFF480ECN.bed.gz'
                   gzip -d PML.bed.gz
                   sort -k 1,1 -k2,2n PML.bed > sorted_PML.bed
                   bgzip -c sorted_PML.bed >sorted_renamed_PML.bed.gz
                   
                   wget https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz
                   gzip -d ZBTB11.bed.gz
                   sort -k 1,1 -k2,2n ZBTB11.bed > sorted_ZBTB11.bed
                   bgzip -c sorted_ZBTB11.bed >sorted_renamed_ZBTB11.bed.gz
                   
                   wget -O ATAC-seq.bed.gz 'https://www.encodeproject.org/files/ENCFF654BVB/@@download/ENCFF654BVB.bed.gz'
                   gzip -d ATAC-seq.bed.gz
                   sort -k 1,1 -k2,2n ATAC-seq.bed > sorted_ATAC-seq.bed
                   bgzip -c sorted_ATAC-seq.bed >sorted_renamed_ATAC-seq.bed.gz
                   
                   wget -O MYB.bed.gz 'https://www.encodeproject.org/files/ENCFF208DZU/@@download/ENCFF208DZU.bed.gz'
                   gzip -d MYB.bed.gz
                   sort -k 1,1 -k2,2n MYB-seq.bed > sorted_MYB-seq.bed
                   bgzip -c sorted_MYB.bed >sorted_renamed_MYB.bed.gz
                   
                   
                   #нужно проиндексировать
                   
                   for i in *sorted_renamed.bed.gz; do tabix -p bed $i; done
                   
                   #устанавливаем геномный браузер в папку mnt/JBrowse
                   cd ../..
                   cd mnt/
                   sudo mkdir JBrowse
                   sudo wget https://github.com/GMOD/jbrowse-components/releases/download/v2.3.2/jbrowse-web-v2.3.2.zip
                   sudo apt-get install unzip
                   sudo unzip jbrowse-web-v2.3.2.zip
                   sudo rm jbrowse-web-v2.3.2.zip
                   
                   #npm install -g @jbrowse/cli 
                   
                   #скачиваем nginx в ver/www/html
                   sudo apt install nginx
                   #изменим конфиг
                   sudo nano /etc/nginx/nginx.conf
                   #перезапуск nginx
                   sudo nginx -s reload
                   
                   sudo jbrowse add-assembly Homo_sapiens.GRCh38.dna.primary_assembly.fa --load copy --out /mnt/JBrowse/
                   sudo jbrowse add-track Homo_sapiens.GRCh38.108.sorted.gff3.gz --load copy --out mnt/JBrowse
                   ssudo jbrowse add-track MYB_sorted_renamed.bed.gz --load copy --out /mnt/JBrowse/
                   sudo jbrowse add-track ZBTB11_sorted_renamed.bed.gz --load copy --out /mnt/JBrowse/
                   sudo jbrowse add-track PML_sorted_renamed.bed.gz --load copy --out /mnt/JBrowse/
                   sudo jbrowse add-track ATAC-seq_sorted_renamed.bed.gz --load copy --out /mnt/JBrowse/


                  
                   
                   
 
 
 
 ссылка  http://158.160.17.228/jbrowse/ работает, ураааа
 
 http://158.160.17.228/jbrowse/?session=local-OOhkfF-4Z
 
 
 


                   
  
                   

                   
                   
                   
                   
                   
                 



                   
                   
                   
             
