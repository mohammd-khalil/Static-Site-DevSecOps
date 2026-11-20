# Kubernetes Deployment

This directory contains the Helm chart and Kubernetes manifests for deploying the application. It is designed to be lightweight for local development while remaining fully compatible with production-grade AWS EKS environments.

## Prerequisites

- **Kubernetes:** v1.19+
- **Helm:** v3.0+
- **Ingress Controller:** Must be installed in the cluster (e.g., NGINX Ingress Controller for local, AWS Load Balancer Controller for EKS).
