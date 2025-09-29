# Pod & Cluster Connections

- **Within the same pod:** Use `localhost`.
- **Within the same cluster:**
  - Get Cluster IP via `kubectl get services`.
  - Use auto-created environment variables (e.g., `process.env.AUTH_SERVICE_SERVICE_HOST` in Node.js).
  - Use CoreDNS for internal service names (e.g., `auth-service.default.svc.cluster.local`).