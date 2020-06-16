# Study_springboot2-webservice
## AWS 설정

### 1. EC2 서버에 접속하기(windows 환경)

1. putty 다운로드(https://www.putty.org/)
2. puttygen 실행
   - pem -> ppk 변경
     - Conversions - Import Key
     - pem 키 선택 -> Save private key 버튼 -> 경고 창 '예(Y)'
     - ppk 저장 위치 선택, 이름 작성 후 저장
3. putty 실행
   - Session 설정
     - HostName : username@public_ip
       - ex) ec2-user@탄력적 IP
     - Port : SSH 접속 포트인 22
     - Connection type : SSH
   - Auth 설정
     - Category - Connection - SSH - Auth
       - Private key file for authentication - 'Browse...' 버튼
   - Saved Sessions에 이름 저장 후 Save
4. 접속
   - Open
   - '예(Y)' 버튼

<br>

### 2. 리눅스 1 서버 생성 시 꼭 해야 할 설정들

1. Java 8 설치

   ```
   sudo yum install -y java-1.8.0-openjdk-devel.x86_64
   ```

   설치 후, 인스턴스의 Java 버전을 8로 변경

   ```
   sudo /usr/sbin/alternatives --config java
   ```

   ![](./docs_images/instance_java.png)

   Java 8을 선택(2 입력)

   버전이 변경 되었으면 사용하지 않는 Java7을 삭제

   ```
   sudo yum remove java-1.7.0-openjdk
   ```

   현재 버전이 Java8이 되었는지 확인

   ```
   java -version
   ```

   <br>

2. 타임존 변경

   ```
   sudo rm /etc/localtime
   ```

   ```
   sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
   ```

   이후, 변경이 되었는지 확인

   ```
   date
   ```

3. Hostname 변경

   ```
   sudo vim /etc/sysconfig/network
   ```

   HOSTNAME을 원하는 서비스 명으로 변경 후 서버를 재부팅

   ```
   sudo reboot
   ```

   재부팅 완료 후,

   ```
   sudo vim /etc/hosts
   ```

   를 입력 후 아래에 ``127.0.0.1 HOSTNAME`` 를 추가한다.

   그리고, 아래 명령어로 확인을 해본다.

   ```
   curl HOSTNAME
   ```

   등록 실패일 경우 : curl: (6) Could not resolve host ~

   등록 성공일 경우 : curl: (7) Failed to connect to ~  / (80 포트로 실행된 서비스가 없음을 의미)

   