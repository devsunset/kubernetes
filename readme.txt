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

# 쿠버네티스 버젼 선택 

* Docker Desktop for Mac / Windows 
  쿠버네티스 별도로 설치 하지 않아도 됨 
  설정 메뉴에서 쿠버네티스를 활성화 해주기만 하면 됨

  kubectl version --short 

* Minikube
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

* 여러 서버로 구성된 쿠버네티스 클러스터 설치 




    

    

