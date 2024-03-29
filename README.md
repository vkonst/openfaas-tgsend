# openfaas-tgsend
OpenFaas function to send messages/images to Telegram.

Based on _tgsend.sh_ - a bash script that sends messages/images.

### Update configs and/or env params
```
# info on params and configs:
~:$ ./tgsend.sh --help
# config example:
~:$ cat .tgsendrc
# NB: always prefer docker/k8s/openfaas secret to store API token(s)
~:$ cat << _EOF_
# Tokens:
defaultApiToken=999999999:fffffffffffffffffffffffffffffffffff
adminBotToken=888888888:eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
# Chats:
mike=333333333
team='-777777777'
_EOF_ | faas secret create tgsend
```
### Build docker image:
```
~:$ docker build -t tgsend .
```

### Deploy OpenFaas function:
```
~:$ faas deploy tgsend
```

### Use OpenFaas function:
```
~:$ faas invoke --query msg=- --query chat-nick=teamChat tgsend
Reading from STDIN - hit (Control + D) to stop.
hey there!
```
```
~:$ curl 'http://127.0.0.1:8080/function/tgsend?msg=-&chat-nick=mike' \
--data-urlencode 'hi there!'
```
