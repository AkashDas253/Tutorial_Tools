## **Logging and Monitoring in Kubernetes**

---

### **Purpose**

Logging and monitoring provide observability into:

* Cluster health
* Application performance
* Infrastructure issues
* Security events

They enable debugging, auditing, alerting, and capacity planning.

---

### **Logging in Kubernetes**

#### **Types of Logs**

* **Application Logs**: Emitted by the app inside containers
* **Node Logs**: System logs from kubelet, kube-proxy, etc.
* **Cluster Logs**: Events from control plane components (API server, etcd)

#### **Log Storage**

* By default, logs are written to **stdout/stderr**.
* Kubelet stores logs in:

  ```
  /var/log/pods/
  /var/log/containers/
  ```
* Logs are ephemeral; they are deleted if the pod is removed.

---

### **Centralized Logging Solutions**

Used to collect, parse, and store logs cluster-wide.

| Stack          | Components                       | Function                                |
| -------------- | -------------------------------- | --------------------------------------- |
| **EFK**        | Elasticsearch, Fluentd, Kibana   | Logging, indexing, visualizing          |
| **ELK**        | Logstash (instead of Fluentd)    | Same purpose with alternative collector |
| **Loki**       | Grafana Loki + Promtail          | Lightweight, log aggregation            |
| **Fluent Bit** | Fluentd’s lightweight sibling    | Log forwarding                          |
| **Vector**     | Log processing & forwarding tool | Efficient and fast                      |

---

### **Log Collection Agents**

* **Deployed as DaemonSets** on all nodes
* Watch `/var/log/containers/` and forward logs to backends

---

### **Monitoring in Kubernetes**

#### **Key Metrics Sources**

* **cAdvisor**: Container resource usage
* **kubelet**: Node and pod-level metrics
* **metrics-server**: Exposes CPU/memory for autoscalers
* **Kube State Metrics**: High-level cluster object metrics

---

### **Monitoring Tools**

| Tool                                      | Purpose                            |
| ----------------------------------------- | ---------------------------------- |
| **Prometheus**                            | Time-series database for metrics   |
| **Grafana**                               | Dashboarding and alerting frontend |
| **Thanos**                                | Prometheus long-term storage       |
| **VictoriaMetrics**                       | Scalable alternative to Prometheus |
| **Datadog**, **New Relic**, **Dynatrace** | Full-stack monitoring platforms    |

---

### **Metrics Types**

| Type        | Examples                                  |
| ----------- | ----------------------------------------- |
| **Node**    | CPU, memory, disk, network                |
| **Pod**     | Usage, restarts, limits, health           |
| **Cluster** | Deployments, replicas, events, API errors |
| **Custom**  | App-specific metrics via `/metrics`       |

---

### **Alerting**

* Prometheus **Alertmanager** supports:

  * Email, Slack, PagerDuty, etc.
  * Alerts based on rules like:

    ```yaml
    expr: rate(http_requests_total[1m]) > 100
    ```
* Grafana also supports integrated alerts.

---

### **Event Monitoring**

* `kubectl get events`
* Helps trace pod creation failures, scheduling issues, crashes

---

### **Best Practices**

* Use **structured logging** in JSON
* Avoid logging sensitive data
* Retain logs securely (encrypt, control access)
* Use **labels** and **correlation IDs** in logs for tracing
* Set resource requests for log collectors to avoid starvation

---
