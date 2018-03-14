# RHOAR Wildfly Swarm Inventory
Demo Microservice for Wildfly Swarm - RHOAR course

## Openshift Deployment
```
export INVENTORY_PROJECT_NAME=swarm-inventory-lab2
oc new-project $INVENTORY_PROJECT_NAME
mvn clean package fabric8:build fabric8:deploy
```

### Deployment Test
```
export INVENTORY_URL=http://$(oc get route swarm-inventory-lab2 -n $INVENTORY_PROJECT_NAME -o template --template='{{.spec.host}}')
curl -X GET "${INVENTORY_URL}/api/inventory/329299"
```

### Database test
```
oc rsh <DATABASE POD NAME>
psql -h localhost --username=$POSTGRESQL_USER -c \
        'select * from INVENTORY' inventory
```