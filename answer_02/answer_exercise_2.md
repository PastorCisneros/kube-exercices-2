# 2.- Ejercicio

## Habilitar el clúster de MongoDB
Creamos el Service
``` kubectl apply -f service.yaml ```


Creamos el StatefulState
``` kubectl apply -f statefulset.yaml ```


Ingresamos a uno de los PODS para habilitar el CLUSTER

``` kubectl exec mongodb-cluster-0 -it bash ```

Configuramos el CLUSTER

``` rs.initiate({_id: "rs0", version: 1, members: [ ```
``` { _id: 0, host : "mongo-statefulset-demo-0.mongodb-service-demo.default.svc.cluster.local:27017" }, ```
``` { _id: 1, host : "mongo-statefulset-demo-1.mongodb-service-demo.default.svc.cluster.local:27017" }, ```
``` { _id: 2, host : "mongo-statefulset-demo-2.mongodb-service-demo.default.svc.cluster.local:27017" } ```
```]}); ```


## Realizar una operación en una de las instancias a nivel de configuración y verificar que el cambio se ha aplicado al resto de instancias

## Diferencias que existiría si el montaje se hubiera realizado con el objeto de ReplicaSet

Si se utiliza el ReplicaSet los pods cambiarían su nombre por lo que el DNS interno no encontraria los nombres configurados en mongo para el cluster (ej. mongo-cluster-0). Ademas a la hora de escalar y desescalar no se haría de manera ordenada si no aleatoria.