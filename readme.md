```
├── php-app
│   └── Dockerfile
└── k8s
    ├── mysql
    │   ├── mysql-statefulset.yaml
    │   └── mysql-secrets.yaml
    ├── redis
    │   └── redis-deployment.yaml
    └── php
        └── php-deployment.yaml
```

# Build

```
docker build -t my-php-app .
```

# Run

```
docker run -d -p 8080:80 my-php-app
```
