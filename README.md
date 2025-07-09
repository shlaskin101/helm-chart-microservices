# Create Helm Chart for Microservices

## 📋 Project Overview

This project demonstrates how to create a reusable **Helm chart** for deploying multiple Kubernetes microservices. The chart uses shared templates for Deployments and Services, enabling you to maintain consistent configurations across microservices while customizing each with environment-specific values.

---

## 🛠️ Technologies Used

- Kubernetes
- Helm

---

## 🎯 Key Concepts

Below are highlights of important Helm concepts and best practices applied in this project:

✅ **`helm create microservice`**

> Command to scaffold a new Helm chart with default templates:

```
helm create microservice
```

This generates:

- `templates/` folder (the YAML templates)
- `values.yaml` (default values for templates)

✅ **Values Object**

- A built-in object that holds configuration values.
- Populated from:

  - `values.yaml`
  - `-f` flag when installing/upgrading (`helm install -f myvalues.yaml ...`)
  - `--set` flag for direct overrides.

✅ **Built-in Objects**
Examples include `Release`, `Files`, `Values`, and more.
Reference:
[Helm Built-in Objects](https://helm.sh/docs/chart_template_guide/builtin_objects/)

✅ **Variable Naming Conventions**

- Use lowercase letters.
- Use camelCase for readability.

✅ **Pipelines**

- Similar to Unix pipelines.
- Used to chain together template functions.

✅ **Helm Rendering Process**

```
/templates → Helm Template Engine → Kubernetes API Server
```

Helm replaces template variables with actual values from all sources.

✅ **helm template**

- Renders chart templates locally.
- Displays YAML output without deploying.

✅ **helm lint**

- Checks charts for possible issues:

```
helm lint -f email-service-values.yaml microservice
```

- **ERROR** = Will fail installation.
- **WARNING** = Breaks conventions.

✅ **helm install**

- Installs chart into the cluster:

```
helm install -f email-service-values.yaml emailservice microservice
```

- `emailservice` is the release name.
- `microservice` is the chart directory.

✅ **--dry-run vs helm template**

- `--dry-run` validates and sends manifests to Kubernetes API (but does not install).
- `helm template` validates and renders locally only.

---

## 🧠 Best Practices Implemented

This project follows production-grade recommendations:

1️⃣ **Pin Image Versions**

- Avoids `latest` tag to ensure predictable deployments.

2️⃣ **Liveness Probes**

- So Kubernetes knows if a container crashes inside a running Pod.

3️⃣ **Readiness Probes**

- So Kubernetes only routes traffic when the app is ready.

4️⃣ **Resource Limits & Requests**

- CPU and Memory requests ensure scheduling.
- Limits prevent a single container from consuming all node resources.

5️⃣ **Avoid NodePort in Production**

- Prefer LoadBalancer or Ingress for safer exposure.

6️⃣ **Multiple Replicas**

- Ensures high availability.

7️⃣ **Multiple Worker Nodes**

- Avoids a single point of failure.

8️⃣ **Labels**

- Consistent labels on resources to enable grouping and selection.

9️⃣ **Namespaces**

- Organizes resources and controls access.

---

## 📂 Project Structure

```
helm-chart-microservices/
├── microservice/            # Helm chart scaffolding
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
├── email-service-values.yaml
└── (other values files)
```

---

## 💡 Next Steps

- Create more values.yaml files for other microservices.
- Integrate CI/CD to automate Helm chart deployments.

---

## ✨ Author

GitHub: [shlaskin101](https://github.com/shlaskin101)

---

## 📜 License

This project is for learning and demonstration purposes.
