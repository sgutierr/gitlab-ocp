# gitlab-ocp
Very minimial Gitlab deployment in OpenShift - Test

## Installation steps
This script contains a minimum installation of Gitlab in OpenShift for testing purposes. The recommendation is run the installation with the Gitlab operator.

Namespace: gitlab

Service Account and Clusterbinding creation 
- oc apply -f gitlab-sa.yml 
- oc apply -f gitlab-clusterbinding.yml
- oc adm policy add-scc-to-user privileged -z gitlab -n gitlab


### Redis: 
note: PV and PVC yml files are not necessary if you already have an OpenShift storage class defined
- #oc apply -f redis/persistent-volume.yml 
- #oc apply -f redis/gitlab-redis-pvc.yml 
- oc apply -f redis/gitlab-redis.yml 
- oc apply -f redis/gitlab-redis-svc.yml 
### Postgresql: 
PV and PVC yml files are not necessary if you already have an OpenShift storage class defined
- #oc apply -f postgresql/persistent-volume-gitlab-postgres.yml
- #oc apply -f postgresql/gitlab-postgresql-pvc.yml 
- oc apply -f postgresql/gitlab-postgresql.yml
- oc apply -f postgresql/gitlab-postgresql-svc.yml

### Gitlab
Set the configmap with your correspondent parameter values:
- oc apply -f gitlab/gitlab-cm.yml
- #oc apply -f gitlab/gitlab-persistent-storage.yml
- #oc apply -f gitlab/gitlab-pvc.yml
Set your secret values:
- oc apply -f gitlab/gitlab-secret.yml
- oc apply -f gitlab/gitlab.yml
- oc apply -f gitlab/gitlab-svc.yml

After run all these steps, you need to create the OpenShift route with gitlab service
