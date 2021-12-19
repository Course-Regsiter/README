# 코드 및 사용자 설명서 (설치 및 실행 가이드)

## 저장소 설명
Frontend: UI 관련 기능  
Backend : 회원가입, 로그인, 토큰 발급 등 인증 관련 기능  
Course-Server: 수강신청 관련 기능  
Infra: 쿠버네티스, 도커 관련 

## Docker 이미지 빌드

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

## Deployment 생성

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

## hpa 설정 (autoscale)

### metrics 서버 설치
```
kubectl create -f metrics-server.yaml
```

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

## 코드 수정
service에서 포트 확인 후 코드에서 데이터베이스 접속, api, cors 수정

### 데이터베이스 접속
파일 경로: Backend/src/index.js

![image](https://user-images.githubusercontent.com/63990390/146634385-a72360a1-fea5-4e83-bff7-16d89c087f17.png)

### cors
파일 경로: Course-Server/src/index.js

![image](https://user-images.githubusercontent.com/63990390/146634409-88fde0cc-b6d4-45ed-87ef-a4df49a24f2d.png)

### api
파일 경로: Frontend/src/api/api.js

![image](https://user-images.githubusercontent.com/63990390/146634492-ab81c000-ab05-405b-a495-354e66101c33.png)  
![image](https://user-images.githubusercontent.com/63990390/146634511-9b7cfb9e-0387-4f10-b422-6c9b20974ddc.png)

## 실행

### 리액트 서버 연결 확인
![image](https://user-images.githubusercontent.com/63990390/146635620-ba9683d6-2d83-42a0-bdf0-fac35d547b19.png)

### 컨테이너 서버 연결 및 데이터베이스 접속 확인
![image](https://user-images.githubusercontent.com/63990390/146634800-da487b49-10aa-4796-98ef-eea4e068cf36.png)

### 몽고디비 작동 확인
![image](https://user-images.githubusercontent.com/63990390/146634873-3fa9d7bb-17e8-49bc-8407-378ca62a62bc.png)  
![image](https://user-images.githubusercontent.com/63990390/146634897-e1008c72-2ff9-435e-853c-849125eb3005.png)

### 웹으로 리액트 서버 접속
![image](https://user-images.githubusercontent.com/63990390/146635678-1d928918-94d5-4eb7-848b-f1102b82a6b3.png)






