-------------------------------------------------

			# KUBERNETES-WORK #

-------------------------------------------------

########################################################
### Kubernetes 

https://kubernetes.io/
https://kubernetes.io/ko/

https://www.docker.com/
https://docs.docker.com/
https://hub.docker.com/

https://docmoa.github.io/02-Private%20Platform/Kubernetes/02-Config/vagrant_k8s.html
https://github.com/Great-Stone/vagrant-k8s

########################################################
### Reference

(시작하세요. 도커/쿠버네티스 book)
https://github.com/alicek106/start-docker-kubernetes

########################################################
### Kubernetes  Guide
(시작하세요. 도커/쿠버네티스 book 요약 정리) 

########################################################
## 소개 
* 쿠버네티스 - 그리스어로 조타수라는 뜻

사실상 표준으로 사용되고 있는 컨테이너 오케스트레이션 도구 
- 도커 스윔 모드 처럼 여러 대의 도커 호스트를 하나의 클러스터로 만들어 준다는 점은 같지만 세부적인 기능을 더욱 폭넓게 제공

# 장점
- 서버 자원 클러스터링 , 마이크로 서비스 구조의 컨테이너 배포, 서비스 장애 복구등 컨테이너 기반의 서비스 운영에 필요한 대부분의
  오케스트레이션 기능을 폭넓게 지원
- 구글,레드햇 등 많은 오픈소스 진영에서 기역 하고 있기 때문에 성능과 안정성 면에서 신뢰 
- 영속적 볼륨, 스케줄링, 장애 복구, 오토 스케일링, 서비스 디스커버리 및 인그레스 등 컨테이너 기반의 클라우드를 운영할 때 필요한 
  기능 과 컴포넌트를 사용자가 커스터 마이징 가능
- CNCF(Cloud Native Computing Foundation) 및 다른 클라우드 운영 도구들과 쉽게 연동 됨으로 확장성 우수 

# 단점
- 휠씬 다양한 지식이 필요 
- 쿠버네티스 자체 관리가 어려울 수도 있음 (소규모 조직에서는 오히려 오버 엔지니어링)

# 종류
- 개발 용도의 쿠버네티스 Minikube (Dockr Desktop for Mac/Windows에 내장된 서비스)
   로컬 노드를 standalone 모드로 사용하기 때문에 쿠버네티스의 기능을 완벽하게 사용해 보기에는 적합하지 않음   
   * 1개의 노드에서 쿠버네티스 설치 및 사용 
   * 간편하게 로컬에서 기본 기능 테스트 가능
   * 쿠버네티스 일부 기능 제한 
- 서비스 테스트 또는 운영 용도의 쿠버 네티스 kops , kubespray, kubeadm , EKS, GKE 등의 Managed 서비스 
  
  * 자체 서버 설치 
     모든 인프라 직접 설치 및 관리 , 원하는 대로 구성 할 수 있다는 장점 , 운영 및 유지 보수가 복잡 해 진다는 단점 
     kubespray, kubeadm 등의 도구를 이용해 쿠버네티스 설치 
  
  * 클라우드 플랫폼 설치
    서버 인스턴스만을 사용해 쿠버네티스 설치 할지 , 쿠버네티스 자체를 서비스로서 제공하는 매니지드 서비스를 사용할지 선택 해야 함
    서버 인스턴스만을 사용 : 서버, 네트워크 등 인프라에 대한 관리는 AWS, GCP 와 같은 클라우드 제공자에게 맡기되 쿠버네티스의 
    설치 및 관리를 직접 수행 ex) AWS EC2 인스턴스를 생성 후 직접 쿠버네티스 설치 kubespray, kubeadm, kops  등의 도구를 이용

        - kubespray, kubeadm 
          - 온프레미스 환경에서 쿠버네티스 설치 가능
          - 클라우드 인프라에서도 쿠버네티스 설치 가능
          * 서버 인프라 및 쿠버네티스 관리가 다소 어려울 수 있음

        - kops
          - 특정 클라우드 플랫폼에 쉽게 쿠버네티스 설치 가능
          - 서버, 네트원크 등 각종 인프라도 자동 프로비저닝

  * 쿠버네티스 자체를 클라우드 서비스로서 사용 
     AWS EKS(Elastic Kubernetes Service), GCP GKE(Google Kubernetes Engine) 등의 매니지드 서비를 이용
     설치 및 관리 까지 클라우드 제공자가 담당 , 관리 및 유지보수 비용이 절감 
     * 설치 필요 없음 가장 쉽게 사용
     * 클라우드 플랫폼에 종송적인 기능도 사용 가능 (로드 밸런서, 퍼시스턴 볼륨 등의 기능)
     * 클라우드 사용 비용 및 의존성 증가
     * 쿠버네티스 자체 학습 하기에는 적합 하지 않음

########################################################
## 설치 

# 쿠버네티스 버젼 선택 

# Docker Desktop for Mac / Windows 
  쿠버네티스 별도로 설치 하지 않아도 됨 
  설정 메뉴에서 쿠버네티스를 활성화 해주기만 하면 됨

  kubectl version --short 

# Minikube
  로컬에서 가상 머신이나 도커 엔진을 통해 쿠버네티스를 사용할 수 있는 환경 제공 

  1) virtualbox 설치
  apt-get install virtualbox
  
  2) minikube, kubectl 내려 받기 
    https://minikube.sigs.k8s.io/docs/start/

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

    curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl

  3) minikube 가상 머신 설치 
    minikube start
    특정 버젼의 쿠버네티스를 설치하려면 --kubernetes-version옵션을 추가
    minikube start --kubernetes-version v1.23.5

        리눅스 서버에서 가상 머신 없이 도커 엔진만으로 minikube설치
        - 도커엔진이 설치된 리눅스에서는 가상 머신 생성하지 않고 Minikube를 이용해 쿠버네티스 설치 할수 있음
          minikube , kubectl 내려 받은 다음 아래 명령어 실행
          minikube start --vm-driver=none

    minikube 삭제 하려면  minikube delete 명령어 사용 

# 여러 서버로 구성된 쿠버네티스 클러스터 설치 
   kubeadm, kops, GKE
   최소한 3대이상 환경 구성 
   - 모든 서버 시간 ntp를 통해 동기화
   - MAC 주소가 각기 다른지 체크
   - 2G Memory , 2 CPU 이상의 충분한 자원
   - swapoff -a 명령어를 통해 메모리 swap을 비 활성화 쿠버네티스 설치 도구는 메모리 스왑을 허용 하지 않음

   * ntp 설정 
   sudo apt-get install -y ntp 
   sudo vi /etc/ntp.conf
      pool 3.ubuntu.pool.ntp.org iburst 하단에 아래 내용 추가 
      server 203.248.240.140 iburst 추가 
      - 동기화 서버 리스트
      time.bora.net (203.248.240.140)
      time.nuri.net (211.115.194.21)
      time2.kriss.re.kr (210.98.16.101)

   ntp 서비스 실행
    sudo systemctl start ntp (서비스 실행)
    sudo systemctl status ntp (서비스 상태 확인)
    ntpq -p (동기화 상태 확인)
    date (시스템 날짜 확인)

    sudo timedatectl set-timezone Asia/Seoul


   마스터 1대  , 워커 노드 3대 구성 

   # kubeadm으로 쿠버네티스 설치 
    쿠버네티스를 쉽게 설치 할 수 있는 관리 도구 
    온프레미스 환경 , 클라우드 인프라 환경 상관 없이 일반적인 리눅스 서버라면 모두 사용 가능 
    
    서버 예시 
    kube-master1 172.31.0.100
    kube-worker1 172.31.0.101
    kube-worker2 172.31.0.102
    kube-worker3 172.31.0.103

    1) 쿠버네티스 저장소 추가 
    모든 노드에서 아래 명령어로 저장소 추가 
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
    cat <<EOF > /etc/apt/source.list.d/kuberenets.list
    deb http://apt.kubernetes.io/ kubernetes-xenial main
    EOF 

    2) containerd 및 kubeadm 설치
      도커를 설치하면 도커에 포함된 containerd가 함께 설치 됨으로 도커에 포함된 containerd를 쿠버네티스와 연동해 사용 

      모든 노드에서 도커를 설치
      wget -q0- get.docker.co | sh 

      도커를 통해 설치된 containerd의 설정 파일은 기본적으로 컨테이너 런타임 인터페이스가 비활성 상태 
      containerd기본 설정값으로 덮어 씌운 뒤 재시작 
      containerd config default > /etc/containerd/config.toml
      service containerd restart

      container (runC)   container (runC)   container (runC)
                                  containerd  <------- kubernetes 
                                  Dockr Engine (docker demon)

    도커 없이 containerd만 설치해도 문제 없이 쿠버네티스를 사용할 수 있음 
    (docker 대신 crictl이라는 명령어를 통해 컨테이너를 제어)
    crictl --runtime-endpoint unix:///run/containerd/containerd.sock ps 
    쿠버네티스는 kubectl을 사용 할수 있음으로 crictl을 사용 하는 경우는 많지 않음 

    모든 노드에서 쿠버네티스에 필요한 패키지 설치
    apt-get install -y kubelet kubeadm kubectl kuberenetes-cni 
   
   3) 쿠버네티스 클러스터 초기화 
   마스터 노드로 사용할 호스트에서 다음 명령어로 클러스터 초기화 
   kubeadm init --apiserver-advertise-address 172.31.0.100 \
   --pod-network-cidr=192.168.0/16 --cri-socket /run/containerd/containerd.sock 

   --apiserver-advertise-address  : 다른 노드가 마스터에 접근할 IP 
   --pod-network-cidr : 쿠버네티스가 사용할 네트워크 대역 
   --cri-socket /run/containerd/containerd.sock  : containerd 런타임 인터페이스를 통해 컨테이너를 사용하도록 설정

  쿠버네티스 1.23까지는 도커 엔진 자체를 컨테이너 런타임 인터페이스로 사용 할 수 있었음
  도커엔진은 컨테이너 런타임 인터페이스를 구현하지 않았으므로 dockershim이라고 불리는 중간 단계를 거쳐야 했음 
  1.24 버전 부터는 도커 엔진을 사용 할수 없게 변경 될 예정 반드시 containerd, cri-o등을 사용 해야 함 

  초기화 처리 되면 출력되는 내용중 중간의 3줄을 복사해 마스터 노드에서 실행
  ...
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kuberenetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config 
  ....

  kubeadm join 172.31.0.100:6443 --token ......

  맨 마지막에 출력된 kubeadm join ... 은 마스터를 제외한 노드인 워커 노드들에서 실행 
  실행시 --cri-socket /run/containerd/containerd.sock 옵션을 명령어 마지막에 추가 
 ex) 
  kubeadm join 172.31.0.100:6443 --token ...... --cri-socket /run/containerd/containerd.sock 

  4) 컨테이너 네트워크 애드온 설치 
  쿠버네티스의 컨테이너 간 통신을 위해 flannel, weaveNet등 여러 오버레이 네트워크를 사용 할 수 있지만 
  예제 에서는 calico를 기준으로 설명
  마스터 노드에서 calico 네트워크 플러그인을 설치 
  kubectl apply -f https://docs.projectcalico.org/v3.22/maifests/calico.yaml

  설치 확인 - STATUS 항목 값이 전부  Running으로 나와야 함
  kubectl get pods --namespace kube-system 
  kubectl get nodes 

kubeadm으로 설치된 쿠버네티스는 각 노드에서 아래 명령어로 삭제 처리 가능 (설치중 오류 발생하거나 테스트용 클러스터 삭제 시 유용)
kubeadm reset 

이전에 설치했던 쿠버네티스 파일들이 /etc/kubernetes 디렉토리에 남아 있는 경우 kubeadm reset명령어로 
초기화 해도 설치시 실패 할수 있음 kubeadm reset 명령어 사용한 뒤 설치시 에러가 발생하면 /etc/kubernetes 삭제 후 재 시도 

# kops로 AWS에서 쿠버네티스 설치 
kops는 클라우드 플랫폼에서 쉽게 쿠버네티스를 설치할 수 있도록 도와 주는 도구 
kubeadm은 서버 인프라를 직접 마련해야 하지만 kops는 서버 인스턴스와 네트워크 리소스 등을 클라우드에서 자동으로 생성해 설치 
kops는 AWS, GCP 등의 클라우드 플랫폼에서 설치를 지원 

1) kops 및 kubectl 실행 바이너리 내려 받기 
wget -O kops https://github.com/kubernetes/kops/releases/download/v1.23.1/kops-linux-amd64
chmod +x ./kops
sudo mv ./kops /usr/local/bin/ 

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

2) AWS 사용자 생성 , 정책 연결 및 AWS CLI 설정 
  네트워크 리소스등 자동으로 생성하기 위해 aws CLI와 AWS 접근 정보 사용 
 ( AWS 문서 참조 )

3) S3 버킷에 쿠버네티스 클러스터의 설정 정보 저장 
kops는 쿠버네티스의 설정 정보를 S3 버킷에 저장 
사용할 S3 버킷을 미리 생성해 두어야 함 

aws s3api create-bucket \
--bucket devsunset-k8s-bucket \
--create-bucket-configuration LocationConstraint=ap-northeast-2

aws s3api put-bucket-versioning \
--bucket devsunset-k8s-bucket \
--versioning-configuration Status=Enabled 

쿠버네티스의 클러스터 이름과 S3 버킷 이름을 환경 변수로서 설정
 export NAME=mycluster.k8s.local
 export KOPS_STATE_STORE=s3://devsunset-k8s-bucket

 쿠버네티스를 설치할 EC2 인스턴스에 배포될 SSH 키를 생성
 ssh-keygen -t rsa -N "" -f ./id_rsa

 클러스터 설정 파일 생성 
 kops create cluster \
 --zones ap-northeast-2a \
 --networking calico \
 --ssh-public-key ./id_rsa.pub \
 $NAME 

 4) 쿠버네티스 클러스터 옵션 변경
 마스터 워커 노드의 인스턴수 타입이나 개수 등 조정 
 kops edit -ig ==name $NAME nodes-ap-northeast-2a 

 5) 쿠버네티스 클러스터 생성
 아래 명령어 입력 하면 자동으로 쿠버네티스가 설치 됨 
 kops update cluster --yes $NAME 

 쿠버 네티스에 접근 할 수 있는 설정 파일 가져오기 
 kops export kubeconfig --admin 

 쿠버네티스 설치 진행 상황 확인 
 kops validate cluster 

 kubectl get node 

 쿠버네시트 삭제 
 kops delete cluster $NAME --yes 


# 구글 클라우드 플랫폼의 GKE로 쿠버네티스 사용하기 
클라우드에서 서비스로 제공하는 GKE , EKS 등  ()

########################################################
##  Vagrant 기반으로 Kubernetes 클러스터  로컬 환경 구성 

https://docmoa.github.io/02-Private%20Platform/Kubernetes/02-Config/vagrant_k8s.html
https://github.com/Great-Stone/vagrant-k8s

git clone https://github.com/Great-Stone/vagrant-k8s.git
cd vagrant-k8s/1.23

RUN example
~/vagrant-k8s/1.23> vagrant up

Check kubeconfig
~/vagrant-k8s/1.23> kubectl --kubeconfig=./.kube/config get nodes

마스터 노드에서 아래 내용 실행
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

########################################################
##  Kubernetes 시작하기 

* 모든 리소스는 오브젝트 형태로 관리 됨 
  컨테이너 집합 (Pods)
  컨테이너 집합을 관리 하는 컴트롤러(Replica Set)
  Service
  Deployment
  ...

오브젝트 조회 명령어 
kubectl api-resources

The connection to the server localhost:8080 was refused - did you specify the right host or port
원인: 마스터노드에서의 kubectl 관련 config가 설정이 되지 않았기 때문 (kubectl config view  출력 내용 확인)
마스터 노드에서 아래 내용 실행
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

오브젝트 설명
kubectl explain 오브젝트 

* 쿠버네티스는 명령어로도 사용 할 수 있지만 YAML 파일을 더 많이 사용 

* 쿠버네티스는 여러 개의 컴포넌트로 구성 
  마스터노드 
    API  서버 (kube-apiserver)
    컨트롤러 매니저 (kube-controller-manager)
    스케쥴러(kube-scheduler)
    DNS서버(coreDNS)
    프락시(kube-proxy)
    네트워크 플러그인(calico, flannel)
crictl --runtime-endpoint unix:///run/containered/containerd.sock ps 
쿠버네티스 클러스터 구성을 위해 kubelet 에이전트 모든 노드에서 실행 

* 쿠버네티스에서 반드시 containerd를 사용해야 할 필요는 없으며 OCI(Open Container Initiative) 라는 컨테이너 런타임 표준을
  구현한 컨테이너 런타임을 갖추고 있다면 사용 가능 

#  파드(Pod) : 컨테이너를 다루는 기본 단위 
   1개 이상의 컨테이너로 구성된 컨테이너 집합 
   여러 개의 컨테이너를 추상화해 하나의 애플리케이션으로 동작 하게 만드는 컨테이너 묶음 

* nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: my-nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
      protocol: TCP

    생성
    kubectl apply -f nginx-pod.yaml 
    pods 확인
    kubectl get pods  
    상세 내용 확인 
    kubectl describe my-nginx-pod
    curl ip값으로 nginx 설치 확인

        클러스터 노드로 접속할 수 없는 상황이라면 
        클러스터 내부에 테스트용 파드를 생성해 임시로 사용 가능
        kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never bash 
        exit로 테스트용 파드에서 빠져나오면 파드는 삭제됨 

    pod 내부로 직접 접속
    kubectl exec -it my-nginx-pod bash
    로그 확인
    kubectl logs my-nginx-pod
    파드 삭제
    kubectl delete -f nginx-pod.yaml or kubectl delete pod <파드명>

  * 파드 vs. 도커 컨테이너 
  쿠버네티스의 파드는 docker run으로 생성된 단일 nginx 컨테이너와 비슷
  파드를 사용 하는 이유는 컨테이너 런타임의 인터페이스 제공 등 여러 가지 이유가 있지만 그 중에 하나는 여러 리눅스 네임스페이스를 공유하는
  여러 컨테이너들을 추상화 된 집합으로 사용 하기 위함 

* nginx-pod-with-ubuntu.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: my-nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
      protocol: TCP

  - name: ubuntu-sidecar-container
    image: alicek106/rr-test:curl
    command: ["tail"]
    args: ["-f", "/dev/null"] # 포드가 종료되지 않도록 유지합니다

  nginx 파드에 2개의 컨테이너가 설치 됨
  -c 옵션을 사용 하여 파드의 특정 컨테이너에 접근 가능 
  kubectl exec -it my-nginx-pod -c ubuntu-sidecar-container bash 
  curl localhost
  우분투 서버에 nginx를 설치 하지 않았는데도 localhost로 접근이 가능 함
  - 파드 내의 컨테이너들이 네트워크 네임스페이스 등과 같은 리눅스 네임스페이스를 공유해 사용하기 때문

* 완전환 애플리케이션으로서의 파드 
  '하나의 파드는 하나의 완전한 애플리케이션'
  사이드카 컨테이너 - 파드에 정의된 부가적인 컨테이너 ex) nginx 컨테이너에 부가적으로 설정변경,로그 수집등의 프로세스가 nginx 컨테이너와 함께 수행 
  파드 냉의 다른 컨테이너와 네트워크 환경을 공유 

* 파드의 네트워크 네임스페이스는 pause라는 이름의 컨테이너로부터 네트워크를 공유 받아 사용
   pause  파드별로 생성되는 컨테이너며 각 파드에 의해 자동으로 생성
   ps aux | grep pause

#  레플리카셋(Replica Set) : 일정 개수의 파드를 유지 하는 컨트롤러 
   파드가 생성된 노드에 장애가 발생하더라도 파드는 다른 노드를 다시 생성하지 않으면 단지 종료된 상태로 유지 됨 
   이런 문제점을 해결하기 위해 레플리카셋과 같이 사용됨 
   
   레플리카셋
   * 정해진 수의 동일한 파드가 항상 실행되도록 관리 
   * 노드 장애 등의 이유로 파드를 사용할 수 없다면 다른 노드에서 파드를 다시 생성 

* replicaset-nginx.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nginx-pods-label
  template:
    metadata:
      name: my-nginx-pod
      labels:
        app: my-nginx-pods-label
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
 
* kubectl api-resources 출력 내용 중 SHORTNAMES 항목으로 명령어를 줄여 사용 할 수 있음
ex) kubectl get pods -> kubectl get po

* replicas: 3 -> replicas: 4 로 변경 후  apply 재 실행 하면 pod가 1개 추가 생성 됨 
kubectl apply -f replicaset-nginx.yaml
replicaset.apps/replicaset-nginx configured

* kubectl delete rs replicaset-nginx 수행하면 레플리카셋에 의해 생성된 파드 또한 함께 삭제 됨 

* 라벨 셀렉터 (Label Selector)
  selector:
    matchLabels:
      app: my-nginx-pods-label

* 이전 버젼의 쿠버네티스에서는 레플리카셋이 아닌 레플리케이션 컨트롤러 라는 오브젝트를 통해 파드의 개수를 유지 

# 디플로이먼트(Deployment) : 레플리카셋, 파드의 배포를 관리 
레플리카셋과 파드의 정보를 정의하는 디플로이먼트 라는 이름의 오브젝트를 YAML 파일에 정의해 사용 
레플리카셋의 상위 오브젝트 디플로이먼트 생성하면 대응 하는 레플리카셋도 함께 생성

* deployment-nginx.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      name: my-nginx-pod
      labels:
        app: my-nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.10
        ports:
        - containerPort: 80

* kubectl apply -f deployment-nginx.yaml
* kubectl get deployment
* kubectl get replicasets
* kubectl get pods
* kubectl delete deploy my-nginx-deployment

* 디플로이먼트를 사용하는 이유 
애플리케이션을 업데이트 할 때 레플리카셋의 변경 사항을 저장하는 리비전을 남겨 롤백을 가능 하게 지원
무중단 서비스를 위해 롤링 업데이트의 전략을 지정 가능 

* kubectl apply -f deployment-nginx.yaml --record 
디플로이먼트에서 생성된 파드의 이미지를 변경 한다고 가정
kubectl set image 사용 하여 변경
kubectl set image deployment my-nginx-deployment nginx=nginx:1.11 --record
위의 명령어는 image 항목을 nginx:1.11로 변경 후 kubectl apply -f 명령어로 적용해도 동일하게 변경 
kubectl get replicasets 명령어로 출력하면 2개의 리플리카셋이 출력 됨 
변경하여 새롭게 생성하였으나 이전 레플리카셋은  파드수가 0인 상태로 유지 (리비전으로서 보존)
아래 명령어로 자세히 확인 가능 
kubectl roolout history deployment my-nginx-deployment
이전 버젼으로 롤백 하려고 한다면 아래 명령어로 롤백 처리 
kubectl rollout undo deployment my-nginx-deployment --to-revision=1 
kubectl get replicates --show-labels
kubectl describe deploy my-nginx-deployment

* 리소스 정리 (모두 삭제 처리)
kubectl delete deployment,pods,rs --all

# 서비스(Service) : 파드를 연결하고 외부에 노출 
YAML 파일에서 containerPort 항목을 정의했다고 해서 이 파드가 바로 외부로 노출되는 것은 아님
외부로 노출해 사용자들이 접근하거나, 다른 디플로이먼트의 파드들이 내부적으로로 접근 하려면 서비스라고 부르는 별도의 쿠버네티스 오브젝트를 생성 해야 함 

서비스 기능
* 여러 갱의 파드에 쉽게 접근할 수 있도록 고유한 도메인 이름을 부여
* 여러 개의 파드에 접근할 때, 요청을 분산하는 로드 밸런서 기능을 수행
* 클라우드 플랫폼의 로드 밸런서, 클러스터 노드의 포트 등을 통해 파드를 외부로 노출 

서비스의 종류
* ClusterIP 타입 
쿠버네티스 내부에서만 파드들에 접근할 때 사용 - 외부에서 파드에 접근할 수 없는 서비스 타입 
* Node Port 타입 
파드에 접근할 수 있는 포트를 클러스터의 모든 노드에 동일하게 개방 - 외부에서 파드에 접근할 수 있는 서비스 타입 
접근할 수 있는 포트는 랜덤으로 정해지지만 특정 포트로 접근 하도록 설정할 수도 있음 
* LoadBalancer 타입 
클라우드 플랫폼에서 제공하는 로드 밴런서를 동적으로 프로지저닝해 파드에 연결 - 외부에서 파드에 접근 할 수 있는 서비스 타입 
AWS, GCP 등과 같은 클라우드 플랫폼 환경에서만 사용 가능 


웹에 접속하면 호스트명을 출력해주는 서비스 
* deployment-hostname.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hostname-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webserver
  template:
    metadata:
      name: my-webserver
      labels:
        app: webserver
    spec:
      containers:
      - name: my-webserver
        image: alicek106/rr-test:echo-hostname
        ports:
        - containerPort: 80

kubectl  apply -f deployment-hostname.yaml
kubectl get pods
kubectl get pods -o wide  (IP 값 출력 옵션)
클러스터 노드 중 하나에 접속해 노드에서 curl을 통해 파드로 접근 

* ClusterIP 타입의 서비스 - 쿠버네티스 내부에서만 파드에 접근하기 
* hostname-svc-clusterip.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-clusterip
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
  selector:
    app: webserver
  type: ClusterIP

* spec.selector : selector 항목은 이 서비스에서 어떠한 라벨을 가지는 파드에 접근할 수 있게 만들 것인지 결정
위 예시에서는 app:webserver 라는 라벨을 가지는 파드들의 집합에 접근 할 수 있는 서비스를 생성 
deployment-hostname.yaml 로 생성된 파드는 해당 라벨이 설정되어 있으므로 서비스에 접근 가능한 대상에 추가 됨

* spec.ports.port : 생성된 서비스는 쿠버네티스 내부에서만 사용할 수 있는 공유한 IP(ClusterIP)를 할당 받음
서비스의 IP에 접근할 때 사용할 포트를 설정 

* spec.ports.targetPort : select 항목에서 정의한 라벨에 의해 접근 대상이 된 파드들이 내부적으로 사용하고 있는 포트를 입력 
파드 템플릿에 정의된 containerPort와 같은 값으로 설정 

* spec.type : 서비스가 어떤 타입인지 나타냄 (ClusterIP, NodePort, LoadBalancer)

서비스 목록 
kubectl get services # services 대신 svc 라고 사용 가능 

vagrant@master:~$ kubectl get services
NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
hostname-svc-clusterip   ClusterIP   10.99.231.150   <none>        8080/TCP   5m17s
kubernetes               ClusterIP   10.96.0.1       <none>        443/TCP    23h

클러스터 노드 중 아무곳에서나 접속하여 CLUSTER-IP 값으로 접속  요청 

kubectl run 명령어로 임시 파드를 생성하여 접속 요청 
kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never -- bash
curl 10.99.231.150 --silent | grep Hello
curl hostname-svc-clusterip:8080 --silent | grep Hello (IP 뿐만 아니라 NAME으로도 접근 - 내부 DNS을 구동하고 자동으로 이 DNS를 사용하도록 설정 됨)
(여러번 호출해 보면 서비스와 연결된 여러개의 파드에 자동으로 요청이 분산됨 - 별도의 설정을 하지 않아도 서비스는 연결된 파드에 대해 로드밸런싱을 수행)

서비스의 라벨 셀렉터와 파드의 라벨이 매칭돼 연결되면 자동으로 엔드포인트라고 부르는 오브젝트를 생성 
kubectl get endpoints # endpoints 대신 ep 사용해도 됨 

서비스 삭제 
kubectl delete svc hostname-svc-clusterip
kubectl delete -f hostname-svc-clusterip.yaml 

# NodePort 타입의 서비스 - 서비스를 이용해 파드를 외부에 노출
스윔모드에서 컨테이너를 외부로 노출하는 방식과 비슷
모든 노드의 특정 포트를 개방해 서비스에 접근 하는 방식 

* hostname-svc-nodeport.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-nodeport
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
  selector:
    app: webserver
  type: NodePort

kubectl  apply -f hostname-svc-nodeport.yaml
kubectl get services

vagrant@master:~$ kubectl get services
NAME                    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hostname-svc-nodeport   NodePort    10.98.198.11   <none>        8080:31143/TCP   53s
kubernetes              ClusterIP   10.96.0.1      <none>        443/TCP          25h

31143 모든 노드에서 동일하게 접근할 수 있는 포트를 의미 
kubectl get nodes -o wide
GKE에서 쿠버네티스 사용하는 경우 각 노드의 랜덤한 포트에 접근하기 위해 별도로 방화벽 설정을 추가 해야 함 
AWS에서도 Security Group에 별도의 Inbound 규칙을 추가하지 않으면 접속 안됨 
gcloud compute firewall-rules create temp-nodeport-svc --allow=tcp:31143 # 규칙추가
gcloud compute firewall-rules delete temp-nodeport-svc #규칙삭제 

각 노드에서 개방되는 포트는 기본적으로 30000 ~32768 포트 중에 랜덤으로 설정됨 
(API 서버 컴포넌트의 실행 옵션을 변경하면 포트 범위 설정 가능 --service-node-port-range=30000-35000)
YAML 파일에서 nodePort 항목을 정의 하면 원하는 포트로 선택 가능
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
      nodePort: 31000

kubectl get nodes -o wide
NodePort 타입의 서비스가 ClusterIP의 기능을 포함 하고 있기 때문에 내부 IP와 DNS 이름으로 접속도 가능 

NodePort로 서비스를 외부에 제공하는 경우는 많지 않음
- NodePort에서 포트 번호를 80 또는 443으로 설정하기에 적절하지 않음
- SSL 인증서 적용 , 라우팅 등과 같은 복잡한 설정을 서비스에 적용하기 어려움 
- NodePort서비스 그 자체를 통해 서비스를 외부에 제공하기 보다는 Ingress 부르는 쿠버네티스의 오브젝트를 간접적으로 사용하는 경우가 많음 

특정 클라이언트가 같은 파드로부터만 처리되게 하려면 sessionAffinity: ClientIP로 설정 
spec:
 essionAffinity: ClientIP

# LoadBalancer 타입의 서비스 - 클라우드 플랫폼의 로드 밴런서와 연동하기 
서비스 생성과 동시에 로드 밸런서를 새롭게 생성해 파드와 연결 
클라우드 플랫폼으로부터 도메인 이름과 IP를 할당 받기 때문에 NodePort보다 더욱 쉽게 파드에 접근 
로드 밸런서를 동적으로 생성하는 기능을 제공하는 환경에서만 사용 가능 
(MetalLB, 오픈스택의 LBassB등과 같은 온프레스미 환경에서도 LoadBalancer 타입의 서비스를 사용할 수 있는 방법이 있음)

* hostname-svc-lb.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-lb
spec:
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

쿠버네티스 1.18.0 버전을 기준으로 서비스의 YAML 파일에서 아무런 설정 하지 않으면 AWS의 클래식 로드 밸런서를 생성

NLB(네트워크 로드 밸런서)를 생성하려면 아래와 같이 정의 하면 됨
* hostname-svc-nlb.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-nlb
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: "nlb"
spec:
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

* 온프레스미 환경에서 LoadBalancer 타입의 서비스 사용하기 
MetalLB, 오픈스택과 같은 특수한 환경을 직접 구축 

* 트래픽의 분배를 결정하는 서비스 속성 : externalTrafficPolicy
kubectl get  svc hostname-svc-nodeport -o yaml 
externalTrafficPolicy: Cluster <- 기본 값 해당 값을 Local로 설정하면 
파드가 생성된 노드에서만 파드로 접근할 수 있음 , 로컬 노드에 위치한 파드 중 하나로 요청이 전달 

* hostname-svc-lb-local.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-lb-local
spec:
  externalTrafficPolicy: Local
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

Cluster와 Local 둘다 장단점이 있음
불필요한 네트워크 홉으로 인한 레이턴시나 클라이언트의 IP 보존이 중요하지 않다면 Cluster 사용 
그 반대라면 Local을 사용 

* 요청을 외부로 리다이렉트하는 서비스 : ExternalName 
쿠버네티스를 외부 시스템과 연동해야 할 때는 ExternalName 타입의 서비스를 사용 
서비스가 외부 도메인을 기리키도록 설정 할 수 있음 

* external-svc.yaml (쿠버네티스를 레거시 시스템과 연동시 유용)
apiVersion: v1
kind: Service
metadata:
  name: externalname-svc
spec:
  type: ExternalName
  externalName: my.database.com

  서비스 접근시 외부 서비스로 리다이렉트 처리 해줌 

########################################################
##  Kubernetes 리소스의 관리와 설정

########################################################
##  Ingress

########################################################
##  퍼시스턴트 볼륨(PV) 과 퍼시트턴트 볼륨 클레임 (PVC)

########################################################
##  보안을 위한 인증과 인가 : ServiceAccount와 RBAC

########################################################
##  어플리케이션 배포를 위한 고급 설정

########################################################
##  커스텀 리소스와 컨트롤러 

########################################################
##  파드를 사용하는 다른 오브젝트들

########################################################
##  쿠버네티스 모니터링 





    

    

