# Minecraft Server on K3d

Local Minecraft server running on Kubernetes using k3d.

## Prerequisites

- Docker
- k3d
- kubectl

## Setup

1. Create k3d cluster with port mapping:

```bash
k3d cluster create minecraft-cluster --agents 2 -p "25565:30001@loadbalancer"
```

2. Deploy Minecraft server:

```bash
kubectl apply -f minecraft-pvc.yml
kubectl apply -f minecraft-configmap.yml
kubectl apply -f minecraft-deployment.yml
kubectl apply -f minecraft-service.yml
```

3. Wait for server to start (check logs):

```bash
kubectl logs -f deployment/minecraft-deployment
```

## Connect

Server address: `localhost:30001`

## Configuration

Edit `minecraft-configmap.yml` to change server settings (game mode, MOTD, server type, etc.).

## Cleanup

```bash
k3d cluster delete minecraft
```
