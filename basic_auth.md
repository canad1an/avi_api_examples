## Login to Avi controller and Get list of Pools
### Authorization header is a base64 encode of "admin:password123"
curl --request GET \
  --url https://CONTROLLERIP/api/pool \
  --header 'Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM='


## Login to Avi controller and create a pool 
### Authorization header is a base64 encode of "admin:password123"
  curl --request GET \
  --url https://CONTROLLERIP/api/pool \
  --header 'Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM' \
  --header 'Content-Type: application/json' \
  --cookie csrftoken=X12E45CB63STlp2ykiRFjQ0alanQHgl0 \
  --data '{
            "name": "testpool3",
						"cloud_ref": "/api/cloud?name=aws",
						"tenant_ref": "/api/tenant?name=admin",
            "servers": [
                {
                    "ip": {
                        "addr": "10.10.1.10",
                        "type": "V4"
                    },
                    "port": "80"
                }
            ]
}'
