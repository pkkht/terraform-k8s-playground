# terraform-k8s-playground

Use terraform init, plan and apply to deploy 2 NGINX containers in k8s.

Local setup of k8s context is Rancher desktop

Use this command to get the k8s config info.
kubectl config view --minify  --flatten --context=rancher-desktop > out.txt

The out.txt will have information required for tfvars:

Define the variables in a terraform.tfvars file.

host corresponds with clusters.cluster.server.
client_certificate corresponds with users.user.client-certificate.
client_key corresponds with users.user.client-key.
cluster_ca_certificate corresponds with clusters.cluster.certificate-authority-data.

The most important learning is wait_for_rollout attribute in main.tf file. Initially I didnt set this variable and the apply was running forever and ever. So I killed the process, reset K8s in Rancher and then re-set the tfvars. After setting the attribute as false, then the apply finished in a sec.

The below excerpt is from Hashicorp doc for the wait_for_rollout attribute:
The wait_for_rollout attribute is available on both the kubernetes_deployment and the kubernetes_stateful_set resources. The default value for wait_for_rollout is true, so if that’s the behavior you want, you don’t need to do anything. However, there are cases where you may not expect a rollout to complete before you’re finished applying your Kubernetes configuration. In these cases, you can set wait_for_rollout to false and the Kubernetes provider will move on after the Deployment or StatefulSet have been successfully submitted to Kubernetes.

--------------------
I have attempted to use Pluralith to generate tf graph but not successful in Mac
https://docs.pluralith.com/docs/get-started/run-locally

See the GitHub link:
https://github.com/Pluralith/pluralith-cli/issues/131

I have done upto the step of renaming the file with hyphen instead of underscore.
But when I try to run Pluralith version, the computer says that the software is malicious and to contact the developer. Hmmmmmm!

-----------------------------------
