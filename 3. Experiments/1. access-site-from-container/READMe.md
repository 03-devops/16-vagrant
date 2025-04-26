## 1. Start Vagrant

```bash
vagrant up
vagrant ssh
sudo -i // Change to root admin
```

## 2. Add Dockerfile

- Make a directory named `tween` and create a `Dockerfile` with content

```bash
mkdir tween
vim Dockerfile
:wq
```

- Install Docker (script added in Vagrantfile)

## 3. Build Custom Image

```bash
docker build -t tween-image .
```

## Run Container From Image

```bash
docker run -d -P tween-image
```

## Allow host access to machine

- Enable `private_network` on `Vagrantfile`

## Get current ip address

- Access from address: <ip-address>:<docker-port>

```bash
ip addr show
```
