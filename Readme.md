
```bash
mkdir helm
cd helm
git clone git clone https://github.com/confluentinc/cp-helm-charts.git
```

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

## 위 명령어 실행 후 내부에서 kafka topic 생성 
kafka-client ~
``` 
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --topic customer --create --partitions 3 --replication-factor 3 --if-not-exists
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --topic payment-request --create --partitions 3 --replication-factor 3 --if-not-exists
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --topic payment-response --create --partitions 3 --replication-factor 3 --if-not-exists
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --topic restaurant-approval-request --create --partitions 3 --replication-factor 3 --if-not-exists
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --topic restaurant-approval-response --create --partitions 3 --replication-factor 3 --if-not-exists
```

### topic 확인 
kafka-client ~
```
kafka-topics --zookeeper local-confluent-kafka-cp-zookeeper-headless:2181 --list
```

# 클러스터 제거시
```bash
helm uninstall local-confluent-kafka
```
# 컨테이너 제거
```bash
kubectl delete -f kafka-client.yml
```