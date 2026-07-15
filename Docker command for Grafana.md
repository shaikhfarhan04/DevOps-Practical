If you're using **Windows PowerShell**, follow these steps to run **Grafana** in Docker.

## Step 1: Verify Docker is Running

Open PowerShell and check Docker:

```powershell
docker --version
docker ps
```

If Docker Desktop is not running, start it first.

---

## Step 2: Pull the Grafana Image

```powershell
docker pull grafana/grafana:latest
```

Verify the image:

```powershell
docker images
```

You should see something like:

```
REPOSITORY          TAG       IMAGE ID
grafana/grafana    latest    xxxxxxxxx
```

---

## Step 3: Run the Grafana Container

```powershell
docker run -d `
--name grafana `
-p 3000:3000 `
grafana/grafana:latest
```

Or as a single line:

```powershell
docker run -d --name grafana -p 3000:3000 grafana/grafana:latest
```

---

## Step 4: Verify the Container

```powershell
docker ps
```

Example:

```
CONTAINER ID   IMAGE                     STATUS
abc123         grafana/grafana:latest   Up 20 seconds
```

---

## Step 5: Open Grafana

Open your browser and go to:

```
http://localhost:3000
```

---

## Step 6: Login

Default credentials:

* **Username:** `admin`
* **Password:** `admin`

Grafana will prompt you to change the password on first login.

---

## Step 7: View Container Logs (Optional)

```powershell
docker logs grafana
```

Or follow logs in real time:

```powershell
docker logs -f grafana
```

---

## Step 8: Stop the Container

```powershell
docker stop grafana
```

---

## Step 9: Start the Container Again

```powershell
docker start grafana
```

---

## Step 10: Restart the Container

```powershell
docker restart grafana
```

---

## Step 11: Remove the Container

Stop it first:

```powershell
docker stop grafana
```

Then remove it:

```powershell
docker rm grafana
```

---

## Step 12: Remove the Image (Optional)

```powershell
docker rmi grafana/grafana:latest
```

---

# Persist Grafana Data (Recommended)

To keep dashboards and settings after removing the container:

```powershell
docker run -d `
--name grafana `
-p 3000:3000 `
-v grafana-storage:/var/lib/grafana `
grafana/grafana:latest
```

Or as a single line:

```powershell
docker run -d --name grafana -p 3000:3000 -v grafana-storage:/var/lib/grafana grafana/grafana:latest
```

Check the Docker volume:

```powershell
docker volume ls
```

---

## Useful Docker Commands

```powershell
docker ps
docker ps -a
docker images
docker logs grafana
docker exec -it grafana /bin/bash
docker inspect grafana
docker stats
```

This setup runs Grafana on **[http://localhost:3000](http://localhost:3000)**, with data persisted in the `grafana-storage` Docker volume so your dashboards survive container restarts and recreation.
