# Step 1 – Create Cluster Config File

# run this command 
nano eks-cluster.yaml
# then add the config.yml file data


# ✅ Step 2 – Create Cluster
# Run this single command:

eksctl create cluster -f eks-cluster.yaml

# Wait Time

# This will take around:15 – 25 minutes

aws eks update-kubeconfig --region ap-south-1 --name nagaraj-stable-cluster

# Step 4 – Verify Everything
  kubectl get nodes
# You should see 4 nodes, all:
  Ready
  
# Check system pods
 kubectl get pods -n kube-system

# All should be:
Running

# Check nodegroups
eksctl get nodegroup --cluster nagaraj-stable-cluster --region ap-south-1

# Output:
ng-frontend
ng-backend
ng-app
ng-worker

# Scaling Later (If Needed) You can increase any nodegroup easily:

eksctl scale nodegroup \
  --cluster nagaraj-stable-cluster \
  --name ng-frontend \
  --nodes 2 \
  --region ap-south-1

# 🧹 Cleanup Command (When Done) To delete everything later:

  eksctl delete cluster --name nagaraj-stable-cluster --region ap-south-1


