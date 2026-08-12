## 서버 3개 띄우기
> [!NOTE]
> `spring-pod.yaml`에 `name`만 다르게 해서 3개의 설정을 `---`을 구분선으로 작성 후 아래와 같은 명령어를 입력한다.

```shell
# 쿠버네티스 실행
$ kubectl apply -f spring-deployment.yaml
pod/spring-pod-1 created
pod/spring-pod-2 created
pod/spring-pod-3 created

# Pod 리스트 출력
$ kubectl get pods
NAME           READY   STATUS    RESTARTS   AGE
spring-pod-1   1/1     Running   0          3m38s
spring-pod-2   1/1     Running   0          3m38s
spring-pod-3   1/1     Running   0          3m38s

# Pod 하나하나 지우기
$ kubectl delete pod spring-pod-1
$ kubectl delete pod spring-pod-2
$ kubectl delete pod spring-pod-3
```

<br>

## Deployment 활용

> [!TIP]
> manifest 파일 명은 중요하지 않다.(`spring-pod.yaml` ➡ `spring-deployment.yaml`)

```shell
# deployment 실행
$ kubectl apply -f spring-deployment.yaml
deployment.apps/spring-deployment created

# deployment 확인
$ kubectl get deployment
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
spring-deployment   3/3     3            3           67s

# replicaset 확인
$ kubectl get replicaset
NAME                           DESIRED   CURRENT   READY   AGE
spring-deployment-77fb8d465f   3         3         3       103s

# pods 확인
$ kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
spring-deployment-77fb8d465f-4wzhd   1/1     Running   0          2m
spring-deployment-77fb8d465f-cps2h   1/1     Running   0          2m
spring-deployment-77fb8d465f-q8ns6   1/1     Running   0          2m
```