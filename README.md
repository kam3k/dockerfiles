## Dockerfiles

Build image (for example):
```
$ docker build -t mgallant_dev_opengl:18.04
```

Create container (for example):
```
docker create --runtime=nvidia -it -e DISPLAY=$DISPLAY -e TERM=xterm-256color -e QT_X11_NO_MITSHM=1 -v $HOME/.Xauthority:/home/mgallant/.Xauthority -v $HOME:/home/mgallant/host --net=host --privileged mgallant_dev_opengl:18.04 /bin/zsh
```

Start container (for example):
```
docker container start -i -a --detach-keys "ctrl-q,q" weird_name
```
