### AWS lightsail에서 Node.js 사용하기 !



### Lightsail ubuntu 인스턴스를 만든 상태라고 가정하고 진행하겠습니다 !

>#### node.js 설치하기
>
>1. apt 패키지 관리자 설치
>
>```
>$ sudo apt-get update
>$ sudo apt-get install nodejs
>```
>
>2. npm node.js 패키지 관리자 설치
>
>```
>$ sudo apt-get install npm
>```
>
>3. node 버전 확인하기
>
>```
>$ nodejs -v
>```
>
> #### PPA를 사용하여 설치하기
>
>1. 홈디렉토리에 있는지 확인 후 시작하자
>
>```
>$ cd ~
>$ curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
>```
>
>2. 이 스크립트의 내용을 `nano`(또는 선호하는 텍스트 편집기로) 검사 할 수 있습니다 
>
>```
>$ nano nodesource_setup.sh
>```
>
>3.  아래의 스크립트를 실행 `sudo`
>
>```
>$ sudo bash nodesource_setup.sh
>```
>
>4. Node.js 패키지 설치
>
>```
>$ sudo apt-get install nodejs
>```
>
>5. 일부 `npm`패키지 (예 : 소스 코드를 컴파일해야하는 패키지)가 작동하려면 `build-essential`패키지 를 설치
>
>```
>$ sudo apt-get install build-essential
>```

###  

### NVM을 사용하여 설치하는 방법

>Node.js를 설치하는 대신 "Node.js 버전 관리자" `apt`라는 `nvm`의미 로 특별히 설계된 도구를 사용
>
>1. 소스 패키지를 빌드 할 수있는 소프트웨어 패키지를 가져오기
>
>```
>$ sudo apt-get update
>$ sudo apt-get install build-essential libssl-dev
>```
>
>2. 필수 패키지가 설치되면 [프로젝트의 GitHub 페이지](https://github.com/creationix/nvm) 에서 nvm 설치 스크립트를 가져올 수 있습니다 .
>
>```
>$ curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh -o install_nvm.sh
>```
>
>3. 설치 스크립트 검사
>
>```
>$ nano install_nvm.sh
>```
>
>4. 스크립트 실행
>
>```
>$ bash install_nvm.sh
>```
>
>5. 홈 디렉토리의 하위 디렉토리에 소프트웨어를 설치합니다 `~/.nvm`. 또한 `~/.profile`파일을 사용하기 위해 필요한 줄을 파일에 추가 합니다.
>
>```
>source ~/.profile
>```
>
>6.  nvm을 설치 했으므로 격리 된 Node.js 버전을 설치
>
>```
>nvm ls-remote
>```
>
>```
>...
>        v8.9.0   
>        v8.9.1   
>        v8.9.2   
>        v8.9.3   
>->      v8.9.4   (Latest LTS: Carbon)      
>```
>
>- v8.9.4 설치
>
>```
>$ nvm install 8.9.4
>```
>
>- nvm은 가장 최근에 설치된 버전을 사용하도록 전환
>
>```
>$ nvm use 8.9.4
>```
>
>7. 버전 중 하나를 기본값으로 설정하려면 다음을 입력 할 수 있습니다.
>
>```
>$ nvm alias default 8.9.4
>```
>
>8. 이 버전은 새 세션이 생성 될 때 자동으로 선택됩니다. 다음과 같이 별칭으로 참조 할 수도 있습니다.
>
>```
>$ nvm use default
>```

 

### PM2를 이용하여 서버를 계속 켜두자 !

>1. pm2 설치
>
>```
>$ sudo npm install pm2 -g --unsafe-perm
>```
>
>2.  서버를 다시 시작할 때 pm2 자동 부팅을 설정
>
>```
>$ pm2 startup 
>```
>
>3. systemctl을 사용하여 systemd 장치의 상태를 확인할 수 있습니다.
>
>```
>$ systemctl status pm2
>```
>
>4. 시작 
>
>```
>$ pm2 start "user app"
>```
>
>### 기타 PM2 사용 (선택 사항)
>
>이 명령으로 응용 프로그램을 중지(PM2 응용 프로그램 이름 또는 ID 지정).
>
>```
>$ pm2 stop app_name_or_id
>```
>
>이 명령으로 응용 프로그램을 다시 시작 (PM2 응용 프로그램 이름 또는 ID 지정).
>
>```
>$ pm2 restart app_name_or_id
>```
>
>현재 PM2에서 관리하는 응용 프로그램 목록은 list 하위 명령을 사용하여 조회
>
>```
>$ pm2 list
>```