
# Flux Setup in K3s Cluster

This guide documents the process of setting up Flux in a K3s cluster, as well as common issues and their resolutions.

---

## Prerequisites

1. **K3s Cluster**: Ensure you have a functioning K3s cluster. Verify using:
   ```bash
   kubectl get nodes
   ```
2. **kubectl**: Installed and configured to interact with your cluster.
3. **GitHub Personal Access Token**: Required for repository authentication.

---

## Setup Steps

1. **Bootstrap Flux**:
   Run the following command to bootstrap Flux with your GitHub repository:
   ```bash
   flux bootstrap github \
     --owner=$GITHUB_USER \
     --repository=homeops \
     --branch=main \
     --path=./clusters/my-cluster \
     --personal
   ```

2. **Verify Installation**:
   After bootstrapping, ensure all Flux components are installed:
   ```bash
   kubectl get pods -n flux-system
   ```

3. **Create Git Repository Secret**:
   Create a secret to authenticate with your Git repository:
   ```bash
   flux create secret git flux-system \
     --url=https://github.com/<your-username>/homeops.git \
     --username=<your-username> \
     --password=<your-token>
   ```

---

## Troubleshooting

### Issue: `No route to host`
- **Symptom**: Flux components fail to reconcile due to inability to connect to the API server.
- **Resolution**:
  1. Ensure `coredns` is running:
     ```bash
     kubectl get pods -n kube-system
     ```
  2. Restart the cluster DNS if necessary:
     ```bash
     kubectl rollout restart deployment coredns -n kube-system
     ```

### Issue: `Unauthorized` Errors
- **Symptom**: Flux fails to access the Git repository.
- **Resolution**:
  1. Verify the Git secret:
     ```bash
     kubectl get secret -n flux-system
     ```
  2. Recreate the secret if needed.

### Issue: `CrashLoopBackOff`
- **Symptom**: Flux components enter a crash loop.
- **Resolution**:
  1. Check component logs:
     ```bash
     kubectl -n flux-system logs deploy/<component-name>
     ```
  2. Verify cluster networking and API accessibility.

---

## Additional Notes

- Avoid using Helm unless required for specific use cases.
- For Kustomize, ensure manifests in the Git repository follow Kustomize structure.

## Logs and Debugging

- Use `kubectl logs` to troubleshoot specific components:
  ```bash
  kubectl -n flux-system logs deploy/source-controller
  ```

---

## Contact

For further assistance, consult the [Flux documentation](https://fluxcd.io/docs/) or raise an issue in your Git repository.
