1.  Create the pods based on the CakePHP, MySQL openshift template
// Persistent volume recycler not working correctly, manually remove/recreate
oc delete pv/pv02
cd /opt/nfs/pv02
rm -rf 
oc create -f pv2.yaml

oc new-project college
oc process -n openshift cakephp-mysql-persistent --param-file=college.env | oc create -f -
oc delete route college
oc create route edge --service=college --hostname=college.apps.ocp.ext.io
temporarily add local host table entries to 


2.  Dump the database on local worksation, tranfer it to OCP cluster, and import the data
Used MySQL GUI on Windows to dump the data
Run this from MySQL pod:
[root@baxter ~]# oc cp alvenn.sql mysql-1-gc2jq:/tmp/alvenn.sql
[root@baxter ~]# oc rsh mysql-1-gc2jq
sh-4.2$ mysql -udba -pdbaalv1 alvenn < /tmp/alvenn.sql

3.  Add PHP files to source control
https://stackoverflow.com/questions/46877667/how-to-push-a-new-initial-project-to-github-using-vs-code

