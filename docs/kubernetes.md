# Workshop 4: Docker and Kubernetes on GKE

## 1. Project Information

- Google Cloud Project: project-e0e04765-c8ed-4a4b-854
- GKE Cluster: freight
- Zone: europe-west3-a
- Application: Freight Event Generator

## 2. Kubernetes Deployment

The freight event generator was successfully deployed to Google Kubernetes Engine (GKE).

The application generates JSON shipment events for AIR and OCEAN freight.

## 3. Self-Healing Test

I deleted the running generator Pod using:

kubectl delete pod -l app=generator

Kubernetes automatically created a replacement Pod.

The replacement Pod reached the Running state without manual intervention.

This demonstrates Kubernetes self-healing.

## 4. Scaling Test

I increased the deployment from 1 Pod to 3 Pods.

All three Pods reached the Running state and generated shipment events successfully.

I then scaled the deployment back to 1 Pod.

## 5. Rolling Update

I changed the generator configuration:

- MODE: both to air
- RATE: 1 to 5

The rolling update completed successfully.

The updated application generated AIR shipment events.

## 6. Rollback Test

I used the following command:

kubectl rollout undo deployment/generator

The rollback completed successfully.

After the rollback, the application generated both AIR and OCEAN shipment events again.

## 7. Verification Commands

kubectl get pods -o wide

kubectl rollout history deployment/generator

## 8. Conclusion

The workshop demonstrated Docker container deployment, Kubernetes self-healing, scaling, rolling updates, and rollback on Google Kubernetes Engine.
NAME                         READY   STATUS    RESTARTS   AGE   IP           NODE                             NOMINATED NODE   READINESS GATES
generator-577cb5d787-lwc24   1/1     Running   0          12m   10.88.0.19   gke-freight-main-4e4fea0c-8xzt   <none>           <none>
deployment.apps/generator 
REVISION  CHANGE-CAUSE
2         <none>
3         <none>

