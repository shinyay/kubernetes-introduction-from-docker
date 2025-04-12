# Chapter 6: Creating and Breaking Kubernetes Resources

In this chapter, we’ll explore the creation of Kubernetes resources and intentionally break them to gain a deeper understanding of their behavior and troubleshooting techniques. Learning through controlled failure helps build confidence in managing Kubernetes clusters.

---

## Chapter Objectives

- Learn how to create various Kubernetes resources using YAML manifests
- Understand common failure scenarios and their causes
- Practice intentional failures to observe and troubleshoot resource behavior
- Strengthen your debugging skills with `kubectl` commands

---

## Cartoon Introduction 🎨

**Illustration:**
Captain Kube standing next to a Pod with a “broken” label, explaining to our protagonist how breaking things intentionally can teach valuable lessons.

---

## 6-1. Creating Kubernetes Resources

### Example Deployment Manifest:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: sample-app
  template:
    metadata:
      labels:
        app: sample-app
    spec:
      containers:
      - name: sample-app
        image: nginx
        ports:
        - containerPort: 80
```

Apply the manifest:
```bash
kubectl apply -f deployment.yaml
```

Verify:
```bash
kubectl get deployments
kubectl get pods
```

**Illustration:**
Captain Kube deploying YAML resources and ensuring a healthy status.

---

## 6-2. Breaking Kubernetes Resources

### Scenario 1: Invalid Image Name
Modify the `image` field in the Deployment manifest to an invalid name:
```yaml
image: nginx:invalid-tag
```
Apply the changes and observe the Pods:
```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl describe pod <pod-name>
```

Expected Behavior:
- Pods will fail to pull the image, resulting in a `CrashLoopBackOff` or `ImagePullBackOff` status.

**Illustration:**
Captain Kube showing a Pod struggling to start due to an invalid image.

---

### Scenario 2: Insufficient Resources
Add resource requests/limits that exceed the Node’s capacity:
```yaml
resources:
  requests:
    memory: "16Gi"
  limits:
    memory: "16Gi"
```

Apply the changes and observe:
```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl describe pod <pod-name>
```

Expected Behavior:
- The Pod will remain in the `Pending` state, unable to be scheduled.

**Illustration:**
Captain Kube pointing out a Pod stuck in the Pending state due to resource constraints.

---

## 6-3. Debugging Broken Resources

### Useful Commands:
1. **Check Pod Logs:**
   ```bash
   kubectl logs <pod-name>
   ```
2. **Describe Resources:**
   ```bash
   kubectl describe pod <pod-name>
   ```
3. **Inspect Events:**
   ```bash
   kubectl get events
   ```

### Pro Tip:
Use `kubectl apply -f` to reapply corrected manifests after fixing issues.

**Illustration:**
Captain Kube using a magnifying glass to inspect `kubectl logs` and `kubectl describe` outputs.

---

## Chapter Summary & Key Takeaways

- Creating and breaking resources helps understand Kubernetes behavior.
- Common failures include invalid images, resource constraints, and misconfigurations.
- Debugging tools like `kubectl logs` and `kubectl describe` are essential for resolving issues.
- Controlled experimentation builds troubleshooting confidence.

**Illustration:**
Captain Kube awarding a "Troubleshooting Master" badge to the protagonist.

---

**Quiz Yourself 🤔**
- What happens if a Pod references an invalid image?
- How can you troubleshoot a Pod stuck in the `Pending` state?
- Which command shows detailed information about a resource?

---

**Congratulations! 🎉** You’ve learned to create and troubleshoot Kubernetes resources. In Chapter 7, we’ll focus on creating secure stateless applications.
