## Protect a Kubernetes Cluster with AppArmor

Enable a no-write AppArmor profile that will prevent containers from being able to write to disk, then apply this profile to the password-db Pod's container. This will prevent this container from writing to disk, and will mitigate the risk of any sensitive data being written to disk by this application in the future



Enable the AppArmor profile on the working and master node:

`sudo apparmor_parser apparmor-k8s-deny-write`

`sudo cp apparmor-k8s-deny-write /etc/apparmor.d`

`sudo chown root:root /etc/apparmor.d/apparmor-k8s-deny-write`

Add an annotations:
  annotations:
    container.apparmor.security.beta.kubernetes.io/password-db: localhost/k8s-deny-write