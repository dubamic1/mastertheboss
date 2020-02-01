# WildFly JWT Demo (WIP)

Example of OpenID secured Client with JWT authentication. JWTs are issued by Keycloak and contain
claims with general user information as well as current user roles.

## Run Keycloak
```
docker run --rm  \
   --name keycloak \
   -e KEYCLOAK_USER=admin \
   -e KEYCLOAK_PASSWORD=admin \
   -e KEYCLOAK_IMPORT=/tmp/quarkus-realm.json  -v /tmp/quarkus-realm.json:/tmp/quarkus-realm.json \
   -p 8180:8180 \
   -it quay.io/keycloak/keycloak:7.0.1 \
   -b 0.0.0.0 \
   -Djboss.http.port=8180 \
   -Dkeycloak.profile.feature.upload_scripts=enabled  
```

NOTE: Replace /tmp/quarkus-realm.json with the actual path in your FS where the quarkus-realm.json is located

## Start WildFly
```
./standalone.sh
```

## Deploy the application
```
mvn install wildfly:deploy
```

## Test the application
```
./admin.sh   # Should pass

./user.sh    # Should fail
```
