# 2.- Ejercicio

## Habilitar el clúster de MongoDB
Creamos el Service
``` kubectl apply -f service.yaml ```


Creamos el StatefulState
``` kubectl apply -f statefulset.yaml ```


Ingresamos a uno de los PODS para habilitar el CLUSTER

``` kubectl exec mongodb-cluster-0 -it bash ```

Configuramos el CLUSTER
~~~
 rs.initiate({_id: "rs0", version: 1, members: [ 
 { _id: 0, host : "mongo-statefulset-demo-0.mongodb-service-demo.default.svc.cluster.local:27017" }, 
 { _id: 1, host : "mongo-statefulset-demo-1.mongodb-service-demo.default.svc.cluster.local:27017" }, 
 { _id: 2, host : "mongo-statefulset-demo-2.mongodb-service-demo.default.svc.cluster.local:27017" } 
]}); 
~~~

## Realizar una operación en una de las instancias a nivel de configuración y verificar que el cambio se ha aplicado al resto de instancias

## Diferencias que existiría si el montaje se hubiera realizado con el objeto de ReplicaSet

A la momento de escalar o descalar de haria de forma aleatoria
El ReplicaSet cambia los nombres de los pods del DNS interno por lo que  no encontraria los nombres  en mongo del cluster. .