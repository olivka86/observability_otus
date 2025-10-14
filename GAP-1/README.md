1. Установил стек Mysql/php-fpm/Wordpress/nginx
2. Установил экспортеры для php-fpm, mysql, nginx, nodeexporter и blackbox
3. Установил Prometheus на тот же сервер.
4. Закрыл доступы ко всем экспортерам. Остался доступ только по локальной сети.
5. С помощью Nginx настроил auth_basic для авторизации в prometheus. Зарегистрировал домен и повесил на него SSL сертификат.
6. Установил alertmanager и настроил алерт на метрики из node_exportera и протестировал их работу.
   
   Все экспортеры настроил через бинарники с запуском через systemd, но для php-fpm сделал исключение и запустил его в контейнере.
 ```bash
 docker run -d -it --rm -e PHP_FPM_SCRAPE_URI="tcp://localhost:9001/status" -e WEB_LISTEN_ADDRESS="127.0.0.1:9253" -p 127.0.0.1:9253:9253 hipages/php-fpm_exporter
```
