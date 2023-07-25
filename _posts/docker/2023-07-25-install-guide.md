---
title: k8s v1.22버전 설치
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- k8s v1.22버전 설치
toc: true
toc_sticky: true
toc_label: 목차

article_tag1: k8s v1.22버전 설치
article_tag2: k8s v1.22버전 설치
# article_section: Javascript
# meta_keywords: Rest Spread
last_modified_at: '2023-07-25 09:00:00 +0800'
---

## k8s v1.22버전 설치
### 설치 가이드
설치스펙 :
Windows10, Cpu 6core 이상, Memory 16GB 이상, 인터넷 사용 가능 환경

```bash
1. XShell 설치 : 생성될 Master/Woker Node에 접속할 툴 (기존에 쓰고 있는게 있으면 생략가능)
2. VirtualBox 설치 : VM 및 내부 네트워크 생성 툴
3. Vagrant 설치 및 k8s 설치 스크립트 실행 : 자동으로 VirtualBox를 이용해 VM들을 생성하고, K8S관련 설치 파일들이 실행됨
4. Worker Node 연결 : Worker Node들을 Master에 연결하여 쿠버네티스 클러스터 구축
5. 설치 확인 : Node와 Pod 상태 조회
6. 대시보드 접근 : Host OS에서 웹 브라우저를 이용해 클러스터 Dashboard에 접근
```

#### 1. XShell 설치
- 다운로드 url : https://www.netsarang.com/en/free-for-home-school/
- 설치 후 k8s-master(192.168.56.30:22), k8s-node1(192.168.56.31:22), k8s-node2(192.168.56.32:22) IP 등록

#### 2. VirtualBox 설치
- 6.1.26 버전 다운로드 : https://download.virtualbox.org/virtualbox/6.1.26/VirtualBox-6.1.26-145957-Win.exe
- 다운로드 사이트 : https://www.virtualbox.org/wiki/Downloads

#### 3. Vagrant 설치 및 k8s 설치 스크립트 실행 
##### 3-1) 설치
- 2.2.18 버전 다운로드 : https://releases.hashicorp.com/vagrant/2.2.18/vagrant_2.2.18_x86_64.msi
- 다운로드 사이트 : https://www.vagrantup.com/downloads

##### 3-2) Vagrant 명령 실행
- 윈도우에서 cmd 실행
- k8s 폴더 생성 및 이동
- Vagrantfile 파일 다운로드
```bash
    C:\Users\사용자>mkdir k8s
    C:\Users\사용자>cd k8s 
    C:\Users\사용자\k8s> curl -O https://kubetm.github.io/yamls/k8s-install/Vagrantfile
```
- Vagrant 실행 (5~10분 소요)
```bash
    C:\k8s> vagrant up
```
- vagrant 명령어 참고
```bash
    vagrant up : 가상머신 기동
    vagrant halt : 가상머신 Shutdown
    vagrant ssh : 가상머신 접속 (vagrant ssh k8s-master)
    vagrant destroy : 가상머신 삭제
```
#### 4. Worker Node 연결
##### 4-1) XShell을 통해 master 접속 (id/pw: root/vagrant)
##### 4-2) cat 명령으로 자신에 master 접근 token 확인 및 복사
```bash
[root@k8s-master ~]# cat ~/join.sh
kubeadm join 192.168.56.30:6443 --token bver73.wda72kx4afiuhspo --discovery-token-ca-cert-hash sha256:7205b3fd6030e47b74aa11451221ff3c77daa0305aad0bc4a2d3196e69eb42b7
```
##### 4-3) worker node1 접속 후 토큰 붙여놓기 (id/pw: root/vagrant)
```bash
[root@k8s-node1 ~]# kubeadm join 192.168.56.30:6443 --token bver73.wda72kx4afiuhspo --discovery-token-ca-cert-hash sha256:7205b3fd6030e47b74aa11451221ff3c77daa0305aad0bc4a2d3196e69eb42b7
```
##### 4-4) worker node2 접속 후 토큰 붙여놓기 반복
```bash
[root@k8s-node2 ~]# kubeadm join 192.168.56.30:6443 --token bver73.wda72kx4afiuhspo --discovery-token-ca-cert-hash sha256:7205b3fd6030e47b74aa11451221ff3c77daa0305aad0bc4a2d3196e69eb42b7
```

#### 5. 설치 확인
##### 5-1) XShell을 통해 master 접속 (id/pw = root/vagrant)
##### 5-2) kubectl 명령어
```bash
[root@k8s-master ~]# kubectl get pod -A
[root@k8s-master ~]# kubectl get nodes
```

#### 6. 대시보드 접근
```bash
http://192.168.56.30:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/workloads?namespace=default
```

#### vagrant up 시 encoding 오류는 설치 경로에 한글이 포함된 것으로 환경변수의 path지정으로 해결

#### Dashboard 관련
- Master Node 재기동시 Dashboard에 접속하기 위해선 아래 명령어를 실행해서 Proxy 오픈하기
```bash
[root@k8s-master ~]# nohup kubectl proxy --port=8001 --address=192.168.56.30 --accept-hosts='^*$' >/dev/null 2>&1 &
```
- Dashboard 접근시 ServiceUnavailable 에러 발생시 아래 명령을 통해 기동안된 Pod 확인
```bash
[root@k8s-master ~]# kubectl get pods -A
```