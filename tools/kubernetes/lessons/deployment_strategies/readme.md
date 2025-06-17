## **Deployment Strategies in Kubernetes**

---

### **Purpose**

Deployment strategies control **how updates** (new versions, configuration changes) are rolled out to minimize downtime and ensure stability.

---

### **Rolling Update (Default)**

* Gradually replaces old pods with new ones.
* Ensures **zero downtime** if configured correctly.

```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1   # Number or % of pods that can be unavailable
    maxSurge: 1         # Number or % of extra pods over desired count
```

* **Safe** and commonly used for production workloads.

---

### **Recreate**

* Deletes all old pods **before** creating new ones.
* Causes **downtime** but ensures a clean state.
* Used when:

  * New version must not run alongside old version
  * App doesn't support parallel versions (e.g., database schema migration)

```yaml
strategy:
  type: Recreate
```

---

### **Blue-Green Deployment**

* Runs two environments:

  * **Blue** (current live)
  * **Green** (new version)
* Traffic is switched from blue to green after verification.

**Steps:**

1. Deploy green version alongside blue
2. Test green
3. Switch service or Ingress to point to green
4. Delete blue (optional)

* Pros: Easy rollback, safe testing
* Cons: Requires double resources temporarily

---

### **Canary Deployment**

* Gradually shifts traffic from old to new version in **percentages**.
* Monitors metrics to detect issues.
* Can be manual or automated using:

  * Service mesh (e.g., Istio)
  * Progressive delivery tools (e.g., Argo Rollouts, Flagger)

**Example Flow:**

* 5% traffic → new version
* Wait and observe
* 25%, 50%, 100% → rollout successively

---

### **A/B Testing**

* Routes traffic to different versions based on user attributes.
* Requires advanced routing (e.g., headers, cookies).
* Implemented using:

  * Ingress controllers
  * Service meshes

---

### **Shadow Deployment**

* Sends a copy of real production traffic to the new version.
* Does **not affect live users**.
* Helps in observing performance/behavior without impact.
* Used for testing under real conditions.

---

### **Progressive Delivery Tools**

* Tools to automate complex deployment strategies:

  * **Argo Rollouts**
  * **Flagger**
  * **Spinnaker**
  * **Keptn**

These provide features like:

* Automated rollback on failure
* Traffic shifting
* Metrics-based analysis
* Gate-based promotions

---

### **Best Practices**

* Use **readiness/liveness probes** to avoid routing to broken pods.
* Monitor CPU/memory/logs/errors during rollout.
* Enable **rollback** via `kubectl rollout undo`.

---
