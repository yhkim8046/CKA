## Cluster Upgrade

1. 업그레이드하고자 하는 노드 스케줄링에서 제외하기

```
k cordon <node>
```

2. 매니페스트 파일을 업그레이드 하고자하는 버전으로 수정하기
위치: /etc/apt/sources.list.d/kubernetes.list

3. kubeadm 업그레이드

```
apt update
apt-cache madison kubeadm
apt-get install kubeadm=1.33.0-1.1
kubeadm upgrade plan v1.33.0
kubeadm upgrade apply v1.33.0
```

4. kubelet 업그레이드

```
apt-get install kubelet=1.33.0-1.1
```

5. 서비스 재시작

```
systemctl daemon-reload
systemctl restart kubelet
```
