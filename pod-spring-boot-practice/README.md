# 서버 3개 띄우기
> [!NOTE]
> `spring-pod.yaml`에 `name`만 다르게 해서 3개의 설정을 `---`을 구분선으로 작성 후 아래와 같은 명령어를 입력한다.

```shell
# 쿠버네티스 실행
$ kubectl apply -f spring-pod.yaml
pod/spring-pod-1 created
pod/spring-pod-2 created
pod/spring-pod-3 created

# Pod 리스트 출력
$ kubectl get pods
NAME           READY   STATUS    RESTARTS   AGE
spring-pod-1   1/1     Running   0          3m38s
spring-pod-2   1/1     Running   0          3m38s
spring-pod-3   1/1     Running   0          3m38s
```