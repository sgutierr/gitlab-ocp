# gitlab-ocp
Very minimial Gitlab deployment in OpenShift - Test

This script contains a minimum installation of Gitlab in OpenShift for testing purposes. The recommendation is run the installation with the Gitlab operator.

Namespace: gitlab

Create service account
oc apply -f gitlab-sa.yml 
oc apply -f gitlab-clusterbinding.yml
oc adm policy add-scc-to-user privileged -z gitlab -n gitlab


These scripts (PV and PVC) are not necessary if you have an OpenShift storage class defined
#oc apply -f redis/persistent-volume.yml 
#oc apply -f redis/gitlab-redis-pvc.yml 

oc apply -f redis/gitlab-redis.yml 
oc apply -f redis/gitlab-redis-svc.yml 

These scripts (PV and PVC) are not necessary if you have an OpenShift storage class defined
#oc apply -f postgresql/persistent-volume-gitlab-postgres.yml
#oc apply -f postgresql/gitlab-postgresql-pvc.yml 

oc apply -f postgresql/gitlab-postgresql.yml
oc apply -f postgresql/gitlab-postgresql-svc.yml

Set configmap properties with your correspondent values:
oc apply -f gitlab/gitlab-cm.yml

These scripts (PV and PVC) are not necessary if you have an OpenShift storage class defined
oc apply -f gitlab/gitlab-persistent-storage.yml
oc apply -f gitlab/gitlab-pvc.yml

Set your secret values:
oc apply -f gitlab/gitlab-secret.yml
oc apply -f gitlab/gitlab.yml
oc apply -f gitlab/gitlab-svc.yml

After run all these steps, you need to create the OpenShift route with gitlab service
