## Login to Avi controller 
curl --request POST \
  --url https://CONTROLLERIP/login \
  --header 'Content-Type: application/json' \
  --data '{
	"username": "admin",
	"password": "password123"
}'


## Get Avi Pools 
curl --request GET \
  --url https://CONTROLLERIP/api/pool \
  --header 'Content-Type: application/json' \
  --header 'Referer: https://CONTROLLERIP' \
  --header 'X-Avi-Tenant: admin' \
  --header 'X-Avi-Version: 22.1.5' \
  --header 'X-CSRFToken: XbuMk8CB63STlp2ykiRFjQ0alanQHgl0' \
  --cookie csrftoken=XbuMk8CB63STlp2ykiRFjQ0alanQHgl0


## Logout of the Avi Controller 
  curl --request POST \
  --url https://CONTROLLERIP/logout \
  --header 'Content-Type: application/json' \
  --header 'Referer: https://CONTROLLERIP' \
  --header 'X-Avi-Version: 22.1.5' \
  --header 'X-CSRFToken: XbuMk8CB63STlp2ykiRFjQ0alanQHgl0' \
  --cookie csrftoken=XbuMk8CB63STlp2ykiRFjQ0alanQHgl0
