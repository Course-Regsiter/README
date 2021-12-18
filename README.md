# 코드 및 사용자 설명서 (설치 및 실행 가이드)

## 1. Docker 이미지 빌드

사설 레지스트리 구축 필요

### react 서버
```
docker build -t react-app .
docker tag react-app 192.168.1.10:8443/react-app
docker push 192.168.1.10:8443/react-app
```

### auth 서버
```
docker build -t nodeauth-img .
docker tag nodeauth-img 192.168.1.10:8443/nodeauth-img
docker push 192.168.1.10:8443/nodeauth-img
```

### course 서버
```
docker build -t nodecourse-img .
docker tag nodecourse-img 192.168.1.10:8443/nodecourse-img
docker push 192.168.1.10:8443/nodecourse-img
```

## 2. Deployment 생성

### react 서버
```
kubectl apply -f deployments-react.yaml
```

### auth 서버
```
kubectl apply -f deployments-auth.yaml
```

### course 서버
```
kubectl apply -f deployments.yaml
```

### mongo 서버
```
kubectl apply -f deployments-mongo.yaml
```

## 3. service 생성

### react 서버
```
kubectl apply -f services-react.yaml
```

### auth 서버
```
kubectl apply -f services-auth.yaml
```

### course 서버
```
kubectl apply -f services.yaml
```

### mongo 서버
```
kubectl apply -f services-mongo.yaml
```

## 4. hpa 설정 (autoscale)
metrics 서버 설치 필요

### react 서버
```
kubectl autoscale deployment react-app --min=3 --max=15 --cpu-percent=25
```

### auth 서버
```
kubectl autoscale deployment node-auth-app --min=3 --max=15 --cpu-percent=25
```

### course 서버
```
kubectl autoscale deployment node-course-app --min=3 --max=15 --cpu-percent=25
```

### mongo 서버
```
kubectl autoscale deployment mongo-server --min=3 --max=15 --cpu-percent=25
```

## 5. 코드 수정
service에서 포트 확인 후 코드에서 데이터베이스 접속, api, cors 수정

## 6. 실행
웹에서 프론트엔드 서버로 접속 



