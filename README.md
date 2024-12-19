# HomeOps Repository

This repository contains Kubernetes manifests and configurations to manage applications and services for my home lab setup using GitOps principles with Argo CD.

---

## **Repository Structure**

```plaintext
.
├── applications/          # Application manifests (e.g., Deployments, Services, Ingress)
│   ├── app1/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
│   ├── app2/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
├── base/                  # Base manifests or shared resources
│   ├── namespace.yaml
│   ├── secrets.yaml
│   └── configmaps.yaml
└── argo-cd/               # Argo CD specific configurations
    ├── project.yaml
    └── applications.yaml
```

---

## **Getting Started**

### Prerequisites

1. **Kubernetes Cluster**: Ensure a Kubernetes cluster is running and accessible.
2. **Argo CD**: Install and configure Argo CD in your cluster.
3. **Git Client**: Ensure `git` is installed and authenticated for this repository.

### Cloning the Repository

```bash
git clone https://github.com/PolarisKnight/homeops.git
cd homeops
```

---

## **Deploying Applications**

1. Add or update application manifests in the `applications/` directory.
   - For each application, create a subdirectory containing the necessary Kubernetes manifests.

2. Sync the changes using Argo CD:
   - Log in to the Argo CD web interface.
   - Create a new application, pointing it to the relevant directory in this repository.

---

## **Contributing**

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add your commit message here"
   ```
4. Push the branch:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a Pull Request.

---

## **License**

This repository is licensed under the MIT License. See the `LICENSE` file for more information.

---

## **Acknowledgments**

- [Kubernetes](https://kubernetes.io/)
- [Argo CD](https://argo-cd.readthedocs.io/)
- Open-source tools and the home lab community.
