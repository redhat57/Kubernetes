To deploy a sample application

You can run the sample application on a cluster that has Amazon EC2 nodes only, Fargate pods, or both.

1. If you're deploying to Fargate, create a Fargate profile. If you're not deploying to Fargate skip this step. You can create the profile by running the following command or you can create the profile with the AWS Management Console using the same values for name and namespace that are in the command.

**eksctl create fargateprofile \
    --cluster my-cluster \
    --region region-code \
    --name alb-sample-app \
    --namespace game-2048**


2. Deploy the game 2048 as a sample application to verify that the AWS Load Balancer Controller creates an AWS ALB as a result of the Ingress object.

**kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.2.0/docs/examples/2048/2048_full.yaml**

3. After a few minutes, verify that the Ingress resource was created with the following command.

**kubectl get ingress/ingress-2048 -n game-2048
Output:**

![image](https://user-images.githubusercontent.com/9262073/129318974-23d157f5-cfe5-4050-8e87-08860a9f9de1.png)

**Note**

If your Ingress has not been created after several minutes, run the following command to view the Load Balancer Controller logs. These logs may contain error messages that can help you diagnose any issues with your deployment.

**kubectl logs -n kube-system   deployment.apps/aws-load-balancer-controller**


4. Open a browser and navigate to the ADDRESS URL from the previous command output to see the sample application. If you don't see anything, wait a few minutes and refresh your browser.

5. When you finish experimenting with your sample application, delete it with the following commands.

kubectl delete -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.2.0/docs/examples/2048/2048_full.yaml
