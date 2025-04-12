# Chapter 4: Creating an Application on a Kubernetes Cluster

In this chapter, we’ll take the knowledge you’ve gained so far and apply it to create and deploy your first application on a Kubernetes cluster. By the end of this chapter, you’ll have a functional application running in Kubernetes, exposed to the network, and ready to scale.

---

## Chapter Objectives

- Learn how to define Kubernetes manifests for your application
- Deploy an application using `kubectl`
- Expose your application to the network with a Service
- Scale your application by adjusting the number of replicas
- Verify and troubleshoot your application’s deployment

---

## Cartoon Introduction 🎨

**Illustration:**
Captain Kube standing in front of a miniature Kubernetes city, placing small Pod figurines onto a Node while explaining how applications are deployed.

---

## 4-1. Defining Kubernetes Manifests

Kubernetes uses declarative YAML manifests to define the desired state of applications and resources. Let’s start with a simple Deployment manifest:

**Example Deployment Manifest:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: nginx
        ports:
        - containerPort: 80
```

### Key components:
- **replicas:** Number of Pod replicas to run.
- **selector:** Labels to match Pods created by the Deployment.
- **template.metadata.labels:** Labels assigned to Pods.
- **containers:** The container image and configuration (e.g., ports).

**Illustration:**
Captain Kube holding a blueprint (YAML manifest) with Pods and configurations sketched out.

---

## 4-2. Deploying the Application

To deploy the application, apply the manifest using `kubectl`:

```bash
kubectl apply -f deployment.yaml
```

### Verify the Deployment:
1. Check the Pods:
   ```bash
   kubectl get pods
   ```
2. Check the Deployment:
   ```bash
   kubectl get deployment hello-world
   ```

**Illustration:**
Captain Kube deploying the application with a "kubectl apply" command, watching Pods appear on a cluster diagram.

---

## 4-3. Exposing the Application to the Network

By default, Pods aren’t accessible outside the cluster. Use a Service to expose the application.

**Example Service Manifest:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world-service
spec:
  type: NodePort
  selector:
    app: hello-world
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30007
```

### Apply the Service:
```bash
kubectl apply -f service.yaml
```

### Access the Application:
Find the Node’s IP address:
```bash
minikube ip
```

Access the application in your browser or with `curl`:
```bash
curl http://<node-ip>:30007
```

**Illustration:**
Captain Kube building a road (Service) connecting the application to the outside world.

---

## 4-4. Scaling the Application

Scaling ensures your application can handle increased traffic.

### Scale the Deployment:
```bash
kubectl scale deployment hello-world --replicas=5
```

### Verify the New Pods:
```bash
kubectl get pods
```

**Illustration:**
Captain Kube adding more Pod figurines to handle increased traffic, clearly demonstrating scaling.

---

## 4-5. Troubleshooting the Application

If something goes wrong, use these commands to debug:

1. **Check Pod logs:**
   ```bash
   kubectl logs <pod-name>
   ```
2. **Describe resources:**
   ```bash
   kubectl describe deployment hello-world
   kubectl describe service hello-world-service
   ```
3. **Delete and reapply manifests:**
   ```bash
   kubectl delete -f deployment.yaml
   kubectl apply -f deployment.yaml
   ```

**Illustration:**
Captain Kube inspecting a Pod with a magnifying glass, clearly troubleshooting common issues.

---

## Chapter Summary & Key Takeaways

- Kubernetes manifests define the desired state of applications.
- Deployments manage Pods and ensure the correct number of replicas are running.
- Services expose applications to the network, making them accessible.
- Scaling applications is as simple as adjusting the number of replicas.
- Debugging tools like `kubectl logs` and `kubectl describe` help resolve issues.

**Illustration:**
Captain Kube awarding a "Deployed My First App" badge to the protagonist.

---

**Quiz Yourself 🤔**
- What is the purpose of a Deployment in Kubernetes?
- How do you expose a Pod to the network?
- Which command allows you to scale a Deployment?

---

**Congratulations! 🎉** You’ve successfully deployed your first application on Kubernetes. In Chapter 5, we’ll dive into troubleshooting and using `kubectl` commands to manage your cluster.
