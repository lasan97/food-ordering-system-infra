

```bash
brew install helm
```

# 아래 명령어 실행 전 다음 파일 수정
`/cp-helm-charts/charts/cp-zookeeper/templates/poddisruptionbudget.yaml` 파일 
`apiVersion: policy/v1beta1`를 `apiVersion: policy/v1beta1`로 변경

```bash
 helm install local-confluent-kafka helm/cp-helm-charts --version 0.6.0
```

```bash
kubectl get pods
kubectl apply -f kafka-client.yml 
```

```bash
# kubectl exec -it kafka-client /bin/bash
# 위 명령어 보다 보다 명확한 권장하는 명령어
kubectl exec -it kafka-client -- /bin/bash
```
