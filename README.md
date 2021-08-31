# Installation guide (Frontend and Backend)

Frontend installation (Unzip all dashboards)
```sh
// Open folder one by one
// then open terminal(Linux) or (Gitbash)

// If your using yarn use:
yarn build

// If your using npm use:
npm build

// If you want to configure BASE_URL
// open .env and modify it if your starting local
// if you want to compile it, then modify .env.production
```

Backend installation (Unzip backend)
```sh
// Make sure you installed composer then run this command
composer install

// Backend uses websocket
// You may run using this command
// If you want to run this server long time use supervisord
php artisan websocket:serve

// If you modify BASE_URL of backend
// Open .env and change BASE_URL

// Important note You should modify this according to your setup
WS_HOST=betting.sabong.wedevit.xyz
WS_PORT=8080
WS_ADDRESS=68.183.228.46
```

Note that you should add nginx directive or apache directive proxy_pass depend on your server

If your using nginx server then add this directives
```sh
location /wss/ {
	proxy_pass http://betting.sabong.wedevit.xyz:8080;
	proxy_http_version 1.1;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection "Upgrade";
	proxy_redirect off;
	proxy_read_timeout 86400s;
	proxy_send_timeout 86400s;
	keepalive_timeout 86400s;
	# prevents 502 bad gateway error
	proxy_buffers 8 32k;
	proxy_buffer_size 64k;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto https;
	reset_timedout_connection on;
}
```

Done! Happy Installing
