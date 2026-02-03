# Step 1 – Create Cluster Config File

Run the following command to create the configuration file:

```
nano eks-cluster.yaml
```

Then add the required cluster configuration data into the file and save it.

---

# Step 2 – Create EKS Cluster

Run this single command to create the cluster:

```
eksctl create cluster -f eks-cluster.yaml
```

---

## Wait Time

Cluster creation will take approximately:

**15 – 25 minutes**

---

# Step 3 – Update Kubeconfig

After the cluster is created, configure kubectl to connect to the cluster:

```
aws eks update-kubeconfig --region ap-south-1 --name nagaraj-stable-cluster
```

---

# Step 4 – Verify Everything

### Verify Worker Nodes

Run the following command:

```
kubectl get nodes
```

You should see **4 nodes**, and all should be in:

**Ready** state

---

### Check System Pods

```
kubectl get pods -n kube-system
```

All pods should be in:

**Running** state

---

### Check Node Groups

```
eksctl get nodegroup --cluster nagaraj-stable-cluster --region ap-south-1
```

Expected Output:

- ng-frontend  
- ng-backend  
- ng-app  
- ng-worker  

---

# Scaling Node Groups Later (If Needed)

You can increase the size of any node group easily using:

```
eksctl scale nodegroup \
  --cluster nagaraj-stable-cluster \
  --name ng-frontend \
  --nodes 2 \
  --region ap-south-1
```

---

# Cleanup Command (When Done)

To delete the entire cluster and avoid AWS billing:

```
eksctl delete cluster --name nagaraj-stable-cluster --region ap-south-1
```

---

## End of Document
