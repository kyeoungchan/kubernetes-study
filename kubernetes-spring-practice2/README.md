```shell
# config map 생성
$ kubectl apply -f spring-config.yaml

# deployment도 수정되면 설정 적용
$ kubectl apply -f spring-deployment.yaml

# deployment 재시작
$ kubectl rollout restart deployment spring-deployment

# spring-secret 생성
$ kubectl apply -f spring-secret.yaml

```