## Login to Avi controller 
curl --request POST \
  --url https://CONTROLLERIP/login \
  --header 'Content-Type: application/json' \
  --data '{
	"username": "admin",
	"password": "password123"
}'


## Get Avi Pools 
curl --request POST \
  --url https://CONTROLLERIP/api/httppolicyset \
  --header 'Content-Type: application/json' \
  --header 'Referer: https://CONTROLLERIP' \
  --header 'X-Avi-Tenant: admin' \
  --header 'X-Avi-Version: 22.1.5' \
  --header 'X-CSRFToken: XbuMk8CB63STlp2ykiRFjQ0alanQHgl0' \
  --cookie csrftoken=XbuMk8CB63STlp2ykiRFjQ0alanQHgl0 \
  --data '{
  "http_request_policy": {
    "rules": [
      {
        "enable": true,
        "index": 1,
        "match": {
          "client_ip": {
            "addrs": [
              {
                "addr": "10.10.10.10",
                "type": "V4"
              }
            ],
            "match_criteria": "IS_IN"
          }
        },
        "name": "Rule1",
        "redirect_action": {
          "keep_query": true,
          "port": 80,
          "protocol": "HTTP",
          "status_code": "HTTP_REDIRECT_STATUS_CODE_302"
        }
      }
    ]
  },
  "name": "vs-1-HttpPolicySet1",
  "tenant_ref": "/api/tenant?name=admin"
}'


## Attach Httppolicyset to VS
curl --request PATCH \
  --url https://CONTROLLERIP/api/virtualservice/virtualservice-1b66fb51-98f1-4cba-ba6b-b89f32833a67 \
  --header 'Content-Type: application/json' \
  --header 'Referer: https://CONTROLLERIP' \
  --header 'X-Avi-Tenant: admin' \
  --header 'X-Avi-Version: 22.1.5' \
  --header 'X-CSRFToken: XbuMk8CB63STlp2ykiRFjQ0alanQHgl0' \
  --cookie csrftoken=XbuMk8CB63STlp2ykiRFjQ0alanQHgl0 \
  --data '{
    "add": {
      "http_policies": [
        {
          "http_policy_set_ref": "/api/httppolicyset/httppolicyset-c0f08e78-4768-46ea-93b8-d8edc75136a8",
          "index": 11
        }
      ]
    }
}'

## Logout of the Avi Controller 
  curl --request POST \
  --url https://CONTROLLERIP/logout \
  --header 'Content-Type: application/json' \
  --header 'Referer: https://CONTROLLERIP' \
  --header 'X-Avi-Version: 22.1.5' \
  --header 'X-CSRFToken: XbuMk8CB63STlp2ykiRFjQ0alanQHgl0' \
  --cookie csrftoken=XbuMk8CB63STlp2ykiRFjQ0alanQHgl0
