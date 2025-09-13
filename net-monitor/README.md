# Network Monitoring (netshoot + iftop)

This guide explains how to use the [nicolaka/netshoot](https://github.com/nicolaka/netshoot) Docker image to monitor NAS network traffic with `iftop`.

---

## 📌 Prerequisites

Before running the commands, make sure:

1. **Hardware**
   - A NAS or Linux server with Docker installed.
   - SSH access to the NAS.

2. **Permissions**
   - Administrator/root privileges to run `docker`.
   - Ability to run privileged containers.

3. **Software**
   - Docker version ≥ 19.x (`docker --version`).
   - Internet access to pull images from Docker Hub, or a pre-loaded `nicolaka/netshoot` image.

4. **Network**
   - You know the interface name to monitor (e.g., `eth0`, `eth1`, `eth3`).

---

## 📥 Pull the Image

Download the image directly from Docker Hub:

```bash
docker pull nicolaka/netshoot
```

If the NAS cannot connect to Docker Hub, pull and save the image on another machine:

```bash
# On a machine with internet
docker pull nicolaka/netshoot
docker save -o netshoot.tar nicolaka/netshoot

# Transfer the tar file to the NAS
docker load -i netshoot.tar
```

---

## 🔍 Find the Network Interface

Check available network interfaces:

```bash
ip link show
```

Typical output:

```
1: lo: ...
2: eth0: ...
3: eth1: ...
4: eth3: ...
```

Pick the interface that you want to monitor (e.g., `eth3`).

---

## ▶️ Run the Monitoring Tool

Start a container with `iftop` monitoring `eth3`:

```bash
docker run -it --rm \
  --net=host --pid=host --privileged \
  nicolaka/netshoot iftop -i eth3
```

### Explanation of parameters
- `--rm`: Remove the container after exit.  
- `--net=host`: Use the host’s network namespace.  
- `--pid=host`: Access the host’s process namespace.  
- `--privileged`: Grant extended privileges (required by `iftop`).  
- `iftop -i eth3`: Run `iftop` on interface `eth3`.  

---

## 📊 Using iftop

- The left column shows local and remote hosts.  
- The right columns show bandwidth (2s, 10s, 40s averages).  
- Press `q` or `Ctrl+C` to exit.  

---

## ⚠️ Troubleshooting

1. **`docker: not found`**  
   → Docker is not installed. Install Docker from your NAS app store or package manager.  

2. **`Unable to find image 'nicolaka/netshoot'`**  
   → Pull the image first: `docker pull nicolaka/netshoot`.  

3. **No traffic shown**  
   → Verify you selected the correct interface with `ip link show`.  

4. **Permission denied**  
   → Run the command as root or with `sudo`.  

---

## 💡 Notes

- This method is intended for **temporary diagnostics**, not for long-term monitoring.  
- For continuous monitoring, consider [Netdata](https://www.netdata.cloud/) or a Prometheus + Grafana stack.  
- Do not run `iftop` for long periods on a production NAS with high load, as it consumes system resources.
