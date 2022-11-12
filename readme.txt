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
   - 모든 서버 시간 nlp를 통해 동기화
   - MAC 주소가 각기 다른지 체크
   - 2G Memory , 2 CPU 이상의 충분한 자원
   - swapoff -a 명령어를 통해 메모리 swap을 비 활성화 쿠버네티스 설치 도구는 메모리 스왑을 허용 하지 않음

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




    

    

