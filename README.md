# MongoDB + Mongo Express on Kubernetes (with AWS EBS CSI Storage)

This setup deploys a **MongoDB** database using a StatefulSet and a **Mongo Express** UI using a Deployment on a Kubernetes cluster. It includes persistent storage using **AWS EBS volumes** and services for external access.

---

##  Components

### 1. MongoDB (StatefulSet)
- Deploys MongoDB in a replicated (2 pods) stateful configuration.
- Uses EBS-backed PersistentVolumeClaims for durable storage.
- Credentials set via environment variables.

### 2. Mongo Express (Deployment)
- A web-based UI for managing MongoDB.
- Exposes a LoadBalancer service for external access.
- Connects to MongoDB using the same credentials.

### 3. Services
- `mongodb`: Internal service (ClusterIP: None) for MongoDB StatefulSet.
- `mongo-express`: LoadBalancer service exposing port 80 externally.

### 4. Storage
- A `StorageClass` using the AWS EBS CSI driver (`ebs.csi.aws.com`).
- Volume expansion is enabled.
- PersistentVolumeClaims (PVCs) for each MongoDB replica.

---

##  File Structure

```text
.
├── mongo-deployment.yaml          # MongoDB StatefulSet, Service, and PVC
├── mongo-express-deployment.yaml # Mongo Express Deployment and Service
└── storage-class.yaml             # EBS StorageClass definition
