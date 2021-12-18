# 코드 및 사용자 설명서 (설치 및 실행 가이드)

## 1. Docker 이미지 빌드

사설 레지스트리 구축 필요

### React 서버
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

### React 서버

### auth 서버

### course 서버

### mongo 서버
