# Day 55: Kubernetes Sidecar Containers

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/1_task.png" alt="Image">
</div>

## Content:

> Today I worked on implementing the **Sidecar Container pattern in Kubernetes**. This task helped me understand how multiple containers inside the same Pod can share storage using `emptyDir` volumes and how sidecar containers can be used for specialized tasks like log shipping.

* * *

## 🔹 What I Learned

*   How to create a Pod with multiple containers
    
*   Understanding the **Sidecar Container pattern**
    
*   How `emptyDir` volumes enable data sharing between containers in the same Pod
    
*   Difference between **regular containers** and **init containers**
    
*   How Kubernetes can run a **restartable init container** using `restartPolicy: Always`
    
*   How log collection can be separated from the main application container
    

* * *

## 🔹 Task Requirement

As per the Nautilus DevOps team requirements, I needed to:

Create a Pod with the following details:

| Requirement | Value |
| --- | --- |
| Pod Name | `webserver` |
| Volume Name | `shared-logs` |
| Volume Type | `emptyDir` |
| Main Container | `nginx-container` |
| Main Image | `nginx:latest` |
| Sidecar Container | `sidecar-container` |
| Sidecar Image | `ubuntu:latest` |
| Shared Mount Path | `/var/log/nginx` |

The sidecar container needed to continuously ship nginx access and error logs using the command:

```bash
sh -c "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"
```

All containers needed to be in a **running state**.

* * *

## 🔹 Steps I Followed

### 1\. Connected to the Jump Host

Logged into the jump host where `kubectl` was already configured for Kubernetes cluster access.

Executed:

```bash
kubectl
```

Observed:

*   Kubernetes CLI was accessible
    
*   Cluster connection was configured properly
    
*   Ready to create Kubernetes resources
    

* * *

## 🔹 2. Created the Pod Manifest File

Created a YAML file for the Pod configuration.

Executed:

```bash
vi webserver.yml
```

Added the following configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver

spec:
  volumes:
    - name: shared-logs
      emptyDir: {}

  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

  initContainers:
    - name: sidecar-container
      image: ubuntu:latest
      restartPolicy: Always
      command:
        - sh
        - -c
        - while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done

      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```

* * *

## 🔹 Simple Explanation of the YAML Configuration

| Section | Explanation |
| --- | --- |
| `apiVersion: v1` | Uses Kubernetes core API |
| `kind: Pod` | Creates a Pod resource |
| `metadata` | Defines Pod details |
| `name: webserver` | Name of the Pod |
| `emptyDir` | Temporary shared storage for containers |
| `nginx-container` | Main application container |
| `sidecar-container` | Log shipping container |
| `volumeMounts` | Mounts shared storage into containers |
| `/var/log/nginx` | Shared location for nginx log files |
| `restartPolicy: Always` | Keeps init sidecar container running |

* * *

## 🔹 3. Applied the Manifest File

Executed:

```bash
kubectl apply -f webserver.yml
```

Observed:

```bash
pod/webserver created
```

This confirmed that the Pod was successfully created.

* * *

## 🔹 4. Verified the Pod Configuration

Executed:

```bash
kubectl get pods
```

Observed:

```bash
NAME        READY   STATUS
webserver   2/2     Running
```

Verified Pod details:

```bash
kubectl describe pod webserver
```

Observed:

```bash
Containers:
  nginx-container:
    State: Running

Init Containers:
  sidecar-container:
    State: Running
```

Also verified:

*   Pod status was **Running**
    
*   Shared volume was mounted correctly
    
*   Sidecar container was continuously reading nginx logs
    

* * *



Nice — these are actually **great verification steps**. I'll integrate them naturally into your structure.

Add this section after **"Verified the Pod Configuration"**.

---

## 🔹 5. Tested Log Generation and Sidecar Functionality

To confirm that nginx was generating logs and the sidecar container could access them through the shared volume, I tested the setup from inside the nginx container.

Executed:

```bash
kubectl exec -it -c nginx-container webserver -- bash
```

Moved to the nginx log directory:

```bash
cd /var/log/nginx/
ls
```

Observed:

```bash
access.log  error.log
```

This confirmed that nginx log files were present inside the mounted shared volume.

Next, I generated HTTP requests to create log entries.

Executed:

```bash
curl localhost
```

Observed:

```html
Welcome to nginx!
```

This created a successful **200 OK** access log entry.

Then executed:

```bash
curl localhost/fun
```

Observed:

```html
404 Not Found
```

This generated a **404 error request**, helping verify both access and error logging.

---

### Verified Sidecar Log Shipping

To confirm that the sidecar container was reading logs from the shared volume, executed:

```bash
kubectl logs webserver -c sidecar-container
```

Observed:

* nginx startup logs
* access log entries
* error/404 request logs generated by curl requests

This verified that:

✅ nginx was writing logs to `/var/log/nginx`
✅ `shared-logs` volume was working correctly
✅ sidecar container could continuously read shared log files

---

## 🔹 Understanding What Happened Behind the Scenes

The workflow looked like this:

```plaintext
curl request
↓
nginx processes request
↓
nginx writes logs to /var/log/nginx
↓
shared-logs (emptyDir) stores logs
↓
sidecar-container reads same files
↓
logs become visible via kubectl logs
```

Because both containers mount the same `emptyDir` volume:

```yaml
mountPath: /var/log/nginx
```

they can access the same log files inside the Pod.

---


## 🔹 Understanding Sidecar Containers

### Sidecar Pattern

The **Sidecar Pattern** means running a helper container alongside the main application container.

In this task:

| Container | Responsibility |
| --- | --- |
| `nginx-container` | Serves web pages |
| `sidecar-container` | Collects and ships logs |

This follows the **separation of concerns principle**.

* * *

### Understanding `emptyDir`

`emptyDir` is a temporary volume created when the Pod starts.

Characteristics:

*   Shared by containers in the same Pod
    
*   Exists as long as the Pod exists
    
*   Removed when the Pod is deleted
    

Here it is used to share nginx log files.

* * *

### Understanding `restartPolicy: Always` in initContainers

Normally:

```plaintext
Init Container → Finish → Exit → Main Container Starts
```

But with:

```yaml
restartPolicy: Always
```

Kubernetes treats the init container like a **persistent sidecar**.

Flow becomes:

```plaintext
sidecar-container starts first
↓
keeps running
↓
nginx-container starts
↓
both containers run together
```

* * *

## 🔹 My Understanding

This task helped me understand how Kubernetes supports the **Sidecar Container pattern** for auxiliary services like logging, monitoring, and proxies. Using `emptyDir`, containers inside the same Pod can safely share files without requiring persistent storage.

I also learned how Kubernetes supports **restartable init containers** using `restartPolicy: Always`.

* * *

## 🔹 What I Found Interesting

I found it interesting how Kubernetes allows one container to focus only on serving applications while another container independently handles logs. The combination of **shared volumes**, **multiple containers**, and **restartable init containers** provides a clean and scalable way to implement supporting services inside a Pod.

* * *

### Topics Covered

- ***kubernetes***
- ***kubernetes-sidecar-container***
- ***kubernetes-shared-volume***
- ***kubectl***


**Previous Task**: [Day 54: Kubernetes Shared Volumes ](../Day_54/day_54.md)

**Next Task**: [Day 56: Deploy Nginx Web Server on Kubernetes Cluster](../Day_56/day_56.md)