```bash
docker network create ci-network
```

```bash
version: '3.7'

services:
  sonarqube:
    image: sonarqube # arm64v8/sonarqube
    ports:
      - 9000:9000
    networks:
      - ci-network

volumes:
  sonarqube_data:

networks:
  ci-network:
    external: true
```


```
http://localhost:9000/account/security
```

```bash
docker run \
    --rm \
    -e SONAR_HOST_URL="http://sonarqube:9000/"  \
    -e SONAR_TOKEN="squ_eeccf19393aae95d26e8efb9056fab0603144113" \
    --network=ci-network \
    -v "/home/fernando/apps/notificacion-adjudicaciones:/usr/src" \
    sonarsource/sonar-scanner-cli \
    -Dsonar.projectKey="mi-proyecto-key" \
    -Dsonar.sources="/usr/src"
```

```bash
http://localhost:9000/quality_gates/
```



