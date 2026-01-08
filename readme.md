```bash
docker network create ci-network
```

```bash
services:
  sonarqube:
    image: sonarqube # arm64v8/sonarqube
    ports:
      - 9000:9000
    networks:
      - ci-network
    volumes:
      - sonarqube_data:/opt/sonarqube/data
    restart: always

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
    -e SONAR_TOKEN="squ_7cbc6f4c478bf4e9bb52b497e45fd87cccc77" \
    --network=ci-network \
    -v "/home/fernando/apps/milugar.devlocal":/usr/src \
    sonarsource/sonar-scanner-cli \
    -Dsonar.projectKey="milugar.devlocal" \
    -Dsonar.sources="/usr/src"
```

```bash
http://localhost:9000/quality_gates/
```



