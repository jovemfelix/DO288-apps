
oc new-project ${RHT_OCP4_DEV_USER}-jenkins  --display-name 'CICD'

# view parameteres
oc process --parameters -n openshift jenkins-ephemeral

oc new-app jenkins-ephemeral -p MEMORY_LIMIT=2Gi

oc new-project ${RHT_OCP4_DEV_USER}-movies-dev --display-name 'Movie DEV'
oc new-project ${RHT_OCP4_DEV_USER}-movies-stage --display-name 'Movie STAGE'

# permissions for Jenkins SA
oc policy add-role-to-user edit system:serviceaccount:${RHT_OCP4_DEV_USER}-jenkins:jenkins -n ${RHT_OCP4_DEV_USER}-movies-dev
oc policy add-role-to-user edit system:serviceaccount:${RHT_OCP4_DEV_USER}-jenkins:jenkins -n ${RHT_OCP4_DEV_USER}-movies-stage


# remember to change namespace property from $JENKINS_URL/configure adding your new projects names

${RHT_OCP4_DEV_USER}-movies-dev
${RHT_OCP4_DEV_USER}-movies-stage