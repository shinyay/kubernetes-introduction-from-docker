# Chapter 8: Review: Fixing Your Application

In this chapter, we’ll revisit the concepts and skills you’ve learned so far by reviewing and fixing a broken application deployed on a Kubernetes cluster. This hands-on approach will solidify your troubleshooting and debugging skills in Kubernetes.

---

## Chapter Objectives

- Learn to identify issues in a Kubernetes application
- Use `kubectl` commands to debug and inspect resources
- Fix common issues in deployments, configurations, and networking
- Gain confidence in troubleshooting Kubernetes applications

---

## Cartoon Introduction 🎨

**Illustration:**
Captain Kube standing next to a broken application (a cracked Pod icon), holding a wrench and a magnifying glass, ready to investigate and fix the issues.

---

## 8-1. Identifying Application Issues

The first step in fixing a broken application is identifying what’s wrong. Common symptoms include:
- Pods stuck in `Pending` or `CrashLoopBackOff` states
- Services not exposing applications correctly
- Configuration errors in manifests
- Networking issues causing connectivity failures

**Illustration:**
Captain Kube pointing to a list of symptoms on a whiteboard, emphasizing common issues.

---

## 8-2. Debugging Pods and Containers

Use `kubectl` commands to inspect Pods and containers.

### Check Pod Status:
```bash
kubectl get pods
```

### Describe a Pod:
```bash
kubectl describe pod <pod-name>
```

### View Logs:
```bash
kubectl logs <pod-name>
```

### Access a Container:
```bash
kubectl exec -it <pod-name> -- /bin/sh
```

**Illustration:**
Captain Kube inspecting a Pod with a magnifying glass, finding details in the logs and descriptions.

---

## 8-3. Fixing Deployment Issues

Common Deployment issues include:
- Incorrect image names or tags
- Configuration mismatches
- Insufficient resources

### Example Fix:
Check and update the Deployment manifest:
```yaml
spec:
  containers:
  - name: app-container
    image: correct-image:latest
    resources:
      requests:
        memory: "128Mi"
        cpu: "500m"
      limits:
        memory: "256Mi"
        cpu: "1"
```

Apply the changes:
```bash
kubectl apply -f deployment.yaml
```

**Illustration:**
Captain Kube fixing a Deployment blueprint and redeploying the application.

---

## 8-4. Resolving Service and Networking Problems

### Verify Service Configuration:
Check the Service manifest for correct ports and selectors:
```yaml
spec:
  selector:
    app: correct-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

### Test Connectivity:
Use port-forwarding to test the application locally:
```bash
kubectl port-forward service/<service-name> 8080:80
```

### Debug DNS Issues:
```bash
kubectl exec -it <pod-name> -- nslookup <service-name>
```

**Illustration:**
Captain Kube building a bridge (Service) to connect the application with the outside network.

---

## 8-5. Validating Configuration and Secrets

Misconfigured ConfigMaps and Secrets can cause application failures.

### Check ConfigMaps:
```bash
kubectl get configmaps
kubectl describe configmap <configmap-name>
```

### Check Secrets:
```bash
kubectl get secrets
kubectl describe secret <secret-name>
```

Update the manifests if there are errors:
```yaml
env:
- name: CONFIG_KEY
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: correct-key
```

Apply the changes:
```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
```

**Illustration:**
Captain Kube carefully reviewing a ConfigMap and fixing misconfigured environment variables.

---

## 8-6. Testing the Fixed Application

After making changes, verify that the application is running correctly:
1. Check Pod status:
   ```bash
   kubectl get pods
   ```
2. Test the Service:
   ```bash
   curl http://<service-ip>:<port>
   ```
3. Monitor logs:
   ```bash
   kubectl logs <pod-name>
   ```

**Illustration:**
Captain Kube giving a thumbs-up as the application runs smoothly after the fixes.

---

## Chapter Summary & Key Takeaways

- Troubleshooting involves identifying and fixing issues in Pods, Deployments, Services, and configurations.
- Use `kubectl describe`, `kubectl logs`, and `kubectl exec` to inspect resources and debug problems.
- Fixing issues requires careful review and updates to manifests.
- Always verify that the application is functioning correctly after making changes.

**Illustration:**
Captain Kube awarding a "Troubleshooting Expert" badge to the protagonist.

---

**Quiz Yourself 🤔**
- What command helps you inspect the details of a Pod?
- How do you test a Service locally using `kubectl`?
- What are common misconfigurations in ConfigMaps and Secrets?

---

**Congratulations! 🎉** You’ve mastered the art of troubleshooting Kubernetes applications. In Chapter 9, we’ll dive deeper into understanding the Kubernetes architecture.
