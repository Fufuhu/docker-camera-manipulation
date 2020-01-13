# Using camera(/dev/video0) with Docker & Kubernetes(Especially with k3s) demo


# When you would like to use with docker

```console
$ docker run -d --name mjpg-streamer -p 8080:8080 --device /dev/video0:/mnt/video0 fufuhu/mjpg-streamer:docker-meetup
```

Access URL(http://127.0.0.1:8080/?action=stream) with your browser.
ID & Password is hoge according to mjpg-streamer/Dockerfile.

# When you'd like to use with kubernetes

```console
$ cd resource
$ kubectl apply -f ./
$ kubectl get services
NAME               TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)          AGE
mjpg-streamer-lb   LoadBalancer   10.43.211.181   192.168.1.136   8080:31597/TCP   3m47s
```

EXTERNAL-IP of mjpg-streamer-lb is 192.168.1.136, so
Access URL(http://192.168.1.136:8080/?action=stream) with your browser.
ID & Password is hoge according to mjpg-streamer/Dockerfile.

## With k3s

If you feel troublesome or not familiar with kubernetes,
you can do it with [rancher/k3s](https://github.com/rancher/k3s).

The only prerequisite is Linux machine.

In the terminal, run commands below.
With these command, you'll install k3s 
and get kubernetes single node cluster on your Linux server.

```console
$ wget https://github.com/rancher/k3s/releases/download/v1.17.0%2Bk3s.1/k3s
$ chmod +x k3s
$ sudo mv k3s /usr/local/bin/k3s
$ sudo k3s server
```



# If you'd like to build docker image by yourself

```console
$ cd mjpg-streamer
$ docker build -t your-favorite-repository:and-tag `pwd`
```

