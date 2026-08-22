```shell
# Nest.js 프로젝트를 설치하고 싶은 폴더에서 아래 명령어를 입력한다.
$ nest new nest-server

# 필요한 모듈들 설치
$ npm i

# 서버 실행
$ npm run start
```

### Dockerfile과 .dockerignore 작성 후
```shell
# Docker 이미지 빌드
$ docker build -t nest-server:1.0 .

# Docker 이미지 잘 생성됐는지 확인
$ docker image ls
```

<br>

### 
```shell
# nest-deployment.yaml 작성 후
$ kubectl apply -f nest-deployment.yaml

# deployment 확인
$ kubectl get deployment
NAME              READY   UP-TO-DATE   AVAILABLE   AGE
nest-deployment   4/4     4            4           50s

# pods 확인
$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
nest-deployment-5f5c94b695-jrrr9   1/1     Running   0          56s
nest-deployment-5f5c94b695-lm8g2   1/1     Running   0          56s
nest-deployment-5f5c94b695-n9l7b   1/1     Running   0          56s
nest-deployment-5f5c94b695-pkqft   1/1     Running   0          56s

# nest-service.yaml 작성 후
$ kubectl apply -f nest-service.yaml

# service 확인
$ kubectl get service
NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP   10.96.0.1        <none>        443/TCP          95m
nest-server   NodePort    10.111.226.188   <none>        3000:31000/TCP   5s
```

> [!NOTE]
> 여기까지 실행하면 localhost:31000으로 접속하면 hello world가 나온다.

<br>

### 소스코드 수정 후 배포
```shell
# 버전을 올린 1.1로 Docker 이미지 재 생성
$ docker build -t nest-server:1.1 .
```

> [!IMPORTANT]
> 그 다음 `nest-deployement.yaml`에 image 명에 바뀐 버전을 명시해준다.

```shell
$ kubectl apply -f nest-deployment.yaml
deployment.apps/nest-deployment configured

$ kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
nest-deployment-89f96f77d-82lzx   1/1     Running   0          35s
nest-deployment-89f96f77d-gj4mg   1/1     Running   0          34s
nest-deployment-89f96f77d-sgq2l   1/1     Running   0          34s
nest-deployment-89f96f77d-zcqsj   1/1     Running   0          35s
```
> [!NOTE]
> 이렇게 새롭게 뜬 것들이 보이고 접속해보면 바뀐 것이 배포된 것을 확인할 수 있다.