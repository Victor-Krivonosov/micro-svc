# Компонент

Log-message-processor - это процессор с короткой очередью, написанный на Python. Его единственная цель - считывать сообщения из очереди Redis и выводить их в стандартный вывод.

# Варианты деплоя:

1. Docker compose
-    Заходим в папку с сервисом.
-    Собираем через docker build -f Dockerfile . -t ИМЯ СЕРВИСА
-    Запускаем сначала front, запускаем docker compose up -d
-    Вместе с front запускается zipkin и redis
-    Запускаем остальные сервисы, также через docker compose 
-    Проверяем, что открывается front на 8080, логинимся admin/admin, и все кнопки нажимаются
-    Проверяем с zipkin порт 9411
    
2. Kubectl
-    Запускаем инфру через docker compose up -d  (zipkin и redis)
-    Заходим в папки k8s внутри сервисах, и делаем kubectl create -f .
-    Проверяем, что все установилось верно, заходим на NodePort front 
-    Проверяем что открывается front, логинимся admin/admin, и все кнопки нажимаются
-    Проверяем с zipkin порт 9411

3. Helm
-    Запускаем инфру через docker compose up -d  (zipkin и redis)
-    Заходим в папку helm в каждом сервисе, и делаем helm install ИМЯ-СЕРВИСА .
-    Проверяем, что все установилось верно, заходим на NodePort front 
-    Проверяем что открывается front, логинимся admin/admin, и все кнопки нажимаются
-    Проверяем с zipkin порт 9411