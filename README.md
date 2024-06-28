# sb-cors
CORS 학습을 위한 예시(Ubuntu22.04, Springboot 3, gradle, Java 17)

## 구조 설명



## Installation
### 초기 설정
- CORS 설정이 되어있는 Springboot 프로젝트를 만들고 실행시킴. 그에 필요한 패키지 자동 설치
1. Ubuntu 환경에 접속
1-1. (선택사항) git 이 설치되어있지 않다면 패키지 설치 
```sh
sudo apt update -y
sudo apt upgrade -y
sudo apt install -y git
```
2.  본 repository 를 clone
```sh
git clone https://github.com/ohahohah/sb-cors.git
```
3. repository 디렉토리로 이동 후 `setup-springboot.sh` 를 실행시킴. 
```sh
cd ./sb-cors
chmod +x ./setup-springboot.sh
./setup-springboot.sh
```

### 프로세스 종료 
#### 아래와 같은 화면에서 프로세스를 종료하면 `ctrl + c` 를 입력
```sh

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.0.0)

2024-06-28T05:19:23.951Z  INFO 18849 --- [           main] c.example.corsdemo.CorsDemoApplication   : Starting CorsDemoApplication using Java 17.0.11 with PID 18849 (/home/ubuntu/cors-demo/build/classes/java/main started by ubuntu in /home/ubuntu/cors-demo)
2024-06-28T05:19:23.957Z  INFO 18849 --- [           main] c.example.corsdemo.CorsDemoApplication   : No active profile set, falling back to 1 default profile: "default"
2024-06-28T05:19:25.468Z  INFO 18849 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2024-06-28T05:19:25.484Z  INFO 18849 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2024-06-28T05:19:25.487Z  INFO 18849 --- [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.1]
2024-06-28T05:19:25.714Z  INFO 18849 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2024-06-28T05:19:25.717Z  INFO 18849 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 1684 ms
2024-06-28T05:19:26.433Z  INFO 18849 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2024-06-28T05:19:26.449Z  INFO 18849 --- [           main] c.example.corsdemo.CorsDemoApplication   : Started CorsDemoApplication in 3.072 seconds (process running for 3.816)
<==========---> 80% EXECUTING [54s]
````

#### 다른 터미널에서 프로세스를 종료하려면 `kill -9 [PID]` 를 사용
1. 현재 SpringBoot PID(Process ID) 찾기
  - 전체 프로세스 중에 java 로 실행되고 있는 CorsDemoApplication 애플리케이션 프로세스를 찾음
```sh
ps aux | grep java | grep CorsDemoApplication
```
- 결과 조회화면에서 PID 를 찾음. 예를 들면 아래와 같은 결과일때에는 ubuntu 바로 옆에 적힌 숫자 `18849`가 PID 임. 
```sh
ubuntu@ip-172-31-25-111:~$ ps aux | grep java | grep CorsDemoApplication
ubuntu     18849  1.8 10.3 2134380 100480 ?      Sl   05:19   0:02 /usr/lib/jvm/java-17-openjdk-amd64/bin/java (내용 중간 생략) com.example.corsdemo.CorsDemoApplication
```
2. 프로세스 종료 명령어 입력
```sh
kill -9 18849
```

### 애플리케이션 시작하기
- 초기 시작 후에는 아래 명령어를 사용해 프로젝트를 시작시킴
- 프로젝트 디렉토리로 이동. 기본값은 `cors-demo`
```sh
cd ~/cors-demo
```
- gradle 을 사용해서 실행
```sh
gradle bootRun
```
- 참고. 명령어 오류 
  - 만약 이동한 디렉토리에 소스코드파일과 함께 gradle이 있고, 시스템에도 gradle 설치가 되어있는데 아래와 같은 에러가 발생한다면, gradle 환경 설정 확인 필요. 
  - 정상적인 프로젝트 디렉토리 예시
```sh
ubuntu@ip-172-31-25-111:~/cors-demo$ ls -l
total 16
drwxrwxr-x 5 ubuntu ubuntu 4096 Jun 28 05:19 build
-rw-rw-r-- 1 ubuntu ubuntu  467 Jun 28 05:18 build.gradle
-rw-rw-r-- 1 ubuntu ubuntu   31 Jun 28 05:18 settings.gradle
drwxrwxr-x 3 ubuntu ubuntu 4096 Jun 28 05:18 src
```  
- 오류 메시지 예시
```sh
ubuntu@ip-172-31-25-111:~/sb-cors$ gradle bootRun
Command 'gradle' not found, but can be installed with:
sudo snap install gradle  # version 7.2, or
sudo apt  install gradle  # version 4.4.1-13
See 'snap info gradle' for additional versions.
```
- 아래 명령어로 gradle 환경변수 세팅 후 다시 `gradle bootRun` 실행시키기
```sh
export PATH=$PATH:/opt/gradle/bin
source /etc/profile.d/gradle.sh
```
