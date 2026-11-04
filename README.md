# -1
코디세이 1-1 연습

# 기본 명령어
- pwd: 현 위치
- ls: 목록 (단, ls -l / ls -a 처럼 옵션 형태는 리눅스 방식)
- mkdir: 폴더 생성
- cd: 폴더로 이동
- New-Item 또는 ni: 빈 파일 생성
- "A" > B: A의 내용을 B 파일에 넣기
- cat: 파일 내용 보기
- cp: 파일 복사
- mv: 이름 바꾸기 또는 옮기기(원본 삭제)
- rm: 파일 삭제 
- ; (세미콜론): 여러 명령러를 한 줄에 이어서 실행
- -Force(리눅스 -a): all (숨김 파일, 종료된 것까지 전부)
- Ctrl + C: 지금 실행 중인 명령 멈춰
- whoami: 현재 사용자 이름
- CMD: 컨테이너가 실행될 때 기본으로 할 일
- #: 주석(설명용, 실행 안 됨)
- code: VScode로 파일 열기(편집기에 등장, 내용 작성 편함)  
- ls -l	파일 권한을 자세히 보기 (-l = long)
- ls -ld	디렉토리 자체의 권한 보기 (-d)
- chmod 644	권한을 644로 변경 (chmod = change mode)
- ls -l과 ls -ld 차이: -d 없이 폴더를 보면 폴더 안 내용이 나와요. -d를 붙여야 폴더 자체 권한이 보여요.

**리눅스(≒ubuntu) 전용** 쉘(bash)
  - ls -l: 상세 목록(권한·소유자·크기 표시)  →  PowerShell: Get-ChildItem 또는 dir
  - ls -a: 숨김 파일까지 모두 표시  →  PowerShell: -Force 옵션
  - touch 파일명: 빈 파일 생성  →  PowerShell: New-Item 또는 ni
  - chmod 755 파일명: 권한을 숫자로 변경 (7=rwx, 5=r-x)
   →  PowerShell: icacls / Set-ItemProperty
  - chmod 644 파일명: 소유자만 수정 가능하게 변경
  - chown 사용자 파일명: 파일 소유자 변경  →  PowerShell: icacls
  - man 명령어: 명령어 설명서 보기  →  PowerShell: Get-Help
  - FROM: 어떤 이미지를 바탕으로 시작할지 (여기선 ubuntu)

**권한 읽는 법**
- -rw-r--r--   1 root  root   6  Nov 3 09:26  test.txt   
└┘└--┘ └┘└┘ └┘    
파일종류 권한 소유자 그룹 크기(6바이트="hello"+줄바꿈) 
- 파일종류: - (일반파일) / d (폴더) / l (링크)
- 권한 rw-r--r-- 은 3칸씩: [소유자][그룹][그 외]
  - rw- : 읽기·쓰기 가능, 실행 불가
  - r-- : 읽기만 가능
- 숫자 변환: r=4, w=2, x=1 (더한 값)
  - 7 = rwx (4+2+1)
  - 6 = rw- (4+2)
  - 5 = r-x (4+1)
  - 4 = r-- (4)
  
**Vim 편집기**(git commit을 -m 없이 실행)
- 입력 모드 -> ESC -> 명령 모드 -> i -> 입력 모드
- :: 명령 입력 시작
- w: write(저장)
- q: quit(나가기)
- :q!: 저장 없이 강제로 나가기

**편집기 명령어**
- "```(백틱)"을 문단 위ㆍ아래에 사용: 회색 상자 
- #글자: 글자 커짐 
- ** 글자 **: 굵게 강조
- Ctrl + Shift + V	미리보기 새 탭으로 열기
  Ctrl + K 떼고 V	미리보기 옆에 나란히 열기
- Ctrl + S: 저장
- Ctrl + F: 찾기
- Ctrl + ~ (물결): 터미널 열기/닫기
- Ctrl + /: 주석 처리
- Ctrl + Shift + P: 명령 팔레트 (모든 기능 검색)

**Docker 명령어**
- docker run -it ubuntu bash: 리눅스 컨테이너에 진입
- docker ps: 실행 중인 컨테이너 
- docker run -d: 백그라운드로 컨테이너 실행
- docker ps -a: 종료된 것까지 전부
- docker logs <이름>: 컨테이너 기록 보기(문제 생기면 여기서 원인 찾음)
- docker stats --no-stream: 자원 사용량 1회 확인
- docker images: 이미지 목록
- up : 설정대로 빌드 + 실행
- -d : 백그라운드 실행

# 개발 워크스테이션 구축

## 1. 프로젝트 개요
개발 환경(PowerShell / Docker / Git)을 설치하고
GitHub 저장소를 연결하여 워크스테이션을 구축하는 미션입니다.

## 2. 실행 환경
- **OS**: Windows 11
- **쉘(Shell)**: PowerShell
- **Git 버전**: 2.56.0
- **Docker 버전**: 29.9.2
- **Node 버전**: 26.13.0

## 3. 터미널 조작 실습

### 3-1. 파일 생성 → 내용 입력 → 확인
```
PS ...\-1> pwd
Path
----
...\-1

PS ...\-1> New-Item test.txt
Mode     LastWriteTime        Length Name
----     -------------        ------ ----
-a----   2026-11-04 15:57          0 test.txt

PS ...\-1> "hello" > test.txt
PS ...\-1> cat test.txt
hello
```
- New-Item 직후 Length = **0** (빈 파일)
- `"hello" >` 입력 후 내용이 채워짐 → `cat`으로 확인

### 3-1. 복사 → 이름변경 → 삭제
```
PS ...\-1> cp test.txt copy.txt
PS ...\-1> ls
Mode     Length Name
----     ------ ----
-a----       16 copy.txt
-a----       16 test.txt
...

PS ...\-1> mv copy.txt renamed.txt
PS ...\-1> ls
Mode     Length Name
----     ------ ----
-a----       16 renamed.txt
-a----       16 test.txt
...

PS ...\-1> rm renamed.txt
```
- cp 후 → copy.txt 생김 (복사 확인)
- mv 후 → copy.txt 사라지고 renamed.txt 생김 (이동 = 원본 삭제 확인)
- rm 후 → renamed.txt 사라짐 (삭제 확인)

### 3-2. 파일/디렉토리 권한 실습 (chmod)

ubuntu 컨테이너에서 chmod로 권한을 변경하고 전/후를 비교했다.

#### 파일 권한
```bash
echo "hello" > test.txt; ls -l test.txt
# -rw-r--r--  (초기: 소유자 rw-, 그외 r--)

chmod 755 test.txt; ls -l test.txt
# -rwxr-xr-x  (실행 권한 x 추가)

chmod 644 test.txt; ls -l test.txt
# -rw-r--r--  (원래 권한으로 복구)
```

#### 디렉토리 권한
```bash
mkdir mydir; ls -ld mydir
# drwxr-xr-x  (맨 앞 d = 디렉토리)

chmod 700 mydir; ls -ld mydir
# drwx------  (소유자만 접근 가능)
```

**정리**
- 맨 앞 문자: 파일 `-`, 디렉토리 `d`
- 755 = rwxr-xr-x / 644 = rw-r--r-- / 700 = rwx------

## 4. Docker 설치 · 점검

### 버전 확인
```powershell
PS C:\...\-1> docker --version
Docker version 29.9.2, build a82e528
```

### 데몬 동작 확인 (docker info — 핵심 발췌)
```powershell
PS C:\...\-1> docker info
Client:
 Version:    29.9.2
 Context:    desktop-linux

Server:
 Containers: 15 (Running: 2, Paused: 0, Stopped: 13)
 Images: 7
 Server Version: 29.9.2
 Storage Driver: overlayfs
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 24
 Total Memory: 15.25GiB
 Kernel Version: 6.18.54.1-microsoft-standard-WSL2
```

> ✅ **데몬(서버) 정상 동작 확인**: `Server:` 섹션이 정상 출력됨 = Docker 데몬이 살아있다는 증거.
> (만약 데몬이 꺼져 있으면 `Server:` 대신 에러가 뜸)

## 5. 컨테이너 실습

### 5-1. hello-world 실행
```powershell
PS C:\...\-1> docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

### 5-2. ubuntu 컨테이너 진입 후 명령 실습
```powershell
PS C:\...\-1> docker run -it ubuntu bash
root@d9e1db14b505:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@d9e1db14b505:/# echo "hi"
hi
root@d9e1db14b505:/# exit
exit
```

#### 📝 attach vs exec 관찰 메모
- **exec**: 실행 중인 컨테이너에 *추가로* 진입 (예: `docker exec -it 컨테이너명 bash`)
- **attach**: 컨테이너의 *메인 프로세스*에 직접 연결됨

## 6. Docker 운영 로그

### 컨테이너 실행
```
PS C:\...\-1> docker run -d --name test-nginx -p 8080:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
...
Status: Downloaded newer image for nginx:latest
51627b07f2da...
```

### 실행 확인
```
PS C:\...\-1> docker ps
CONTAINER ID   IMAGE   ...   STATUS         PORTS                      NAMES
51627b07f2da   nginx   ...   Up 12 seconds  0.0.0.0:8080->80/tcp      test-nginx
```

### 로그 확인
```
PS C:\...\-1> docker logs test-nginx
...
2026/11/03 08:24:20 [notice] 1#1: start worker process 31
```

### 자원 사용량
```
PS C:\...\-1> docker stats --no-stream
CONTAINER ID   NAME         CPU %   MEM USAGE / LIMIT    ...   PIDS
51627b07f2da   test-nginx   0.00%   22.23MiB / 15.25GiB  ...   25
```

## 7. Docker 이미지 빌드 (Dockerfile → 커스텀 이미지)

### 파일 구성
- `Dockerfile` : nginx 기반, index.html을 웹 루트에 복사
- `index.html` : 접속 확인용 테스트 페이지

### Dockerfile 본문
```dockerfile
# nginx 이미지를 기반으로 사용
FROM nginx:latest

# 내가 만든 페이지를 nginx 기본 페이지 위치에 복사
COPY index.html /usr/share/nginx/html/index.html
```

### Dockerfile 핵심 명령어
- **FROM**: 바탕이 되는 이미지 지정 (여기선 nginx)
- **COPY**: 로컬 파일을 이미지 안으로 복사 (index.html → 웹 루트)
- (CMD/EXPOSE 등은 nginx 이미지에 기본 설정됨)

**커스텀 포인트**: nginx 공식 이미지를 베이스로 하되, 기본 환영 페이지를
내가 작성한 `index.html`로 덮어써서 나만의 웹페이지를 띄우는 이미지를 만듦.

### 실행 순서

#### 1. 이미지 빌드
```
PS C:\...\-1\docker-practice> docker build -t my-web .
```
- `-t my-web` : 이미지에 `my-web` 이라는 이름(태그) 붙이기
- `.` : 현재 폴더의 Dockerfile 사용

#### 빌드 로그
```
[+] Building 0.4s (7/7) FINISHED
 => [internal] load build definition from Dockerfile
 => => transferring dockerfile: 218B
 => [internal] load metadata for docker.io/library/nginx:latest
 => [1/2] FROM docker.io/library/nginx:latest
 => [2/2] COPY index.html /usr/share/nginx/html/index.html
 => exporting to image
 => => naming to docker.io/library/my-web:latest
```
`naming to ... my-web:latest`로 커스텀 이미지 생성 성공 확인.

#### 2. 컨테이너 실행
```
PS C:\...\-1\docker-practice> docker run -d -p 8080:80 --name web my-web
```
- `-d` : 백그라운드 실행
- `-p 8080:80` : 내 PC 8080 포트 → 컨테이너 80 포트 연결
- `--name web` : 컨테이너 이름 지정

#### 3. 실행 확인
```
PS C:\...\-1\docker-practice> docker ps
CONTAINER ID   IMAGE    COMMAND                   STATUS         PORTS                                     NAMES
b3baf8a94400   my-web   "/docker-entrypoint.…"   Up 3 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web
```

## 8. 포트 매핑 & 웹 접속 확인

### 컨테이너 실행
```powershell
docker run -d -p 8080:80 my-web
```
- `-d` : 백그라운드 실행
- `-p 8080:80` : 호스트의 8080 포트를 컨테이너의 80(nginx) 포트에 연결

### 실행 상태 확인
```powershell
docker ps
```
`0.0.0.0:8080->80/tcp` 로 포트 매핑이 정상 적용된 것을 확인.

### 웹 접속 결과
브라우저에서 `http://localhost:8080` 접속 →
Dockerfile로 커스텀한 `index.html` 페이지가 정상 출력됨.

![웹 접속 화면](<스크린샷 2026-11-04 173304.png>)

## 9. 바인드 마운트 & 볼륨 영속성

### 🎯 목적
컨테이너를 **삭제해도 데이터가 유지되는지** 검증한다.
데이터를 컨테이너가 아닌 **볼륨(mydata)에 분리 보관**하는 것이 핵심.

### 실습 로그
```powershell
# 1) 볼륨 생성
PS> docker volume create mydata
mydata

# 2) 볼륨 연결해 컨테이너 실행
PS> docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
b741ca17290e...

# 3) 볼륨에 파일 생성
PS> docker exec vol-test sh -c "echo hi > /data/hello.txt"

# 4) 삭제 전 확인
PS> docker exec vol-test cat /data/hello.txt
hi

# 5) 컨테이너 완전 삭제
PS> docker rm -f vol-test
vol-test

# 6) 같은 볼륨으로 새 컨테이너 실행
PS> docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity
90a14aaa7617...

# 7) 데이터 생존 확인 ✅
PS> docker exec vol-test2 cat /data/hello.txt
hi   # 컨테이너를 삭제했는데도 데이터가 그대로 유지됨!
```

### 📌 관찰
- 컨테이너(`vol-test`)를 **완전히 삭제**했지만, 볼륨 `mydata`는 독립적으로 유지됨.
- 새 컨테이너(`vol-test2`)에 같은 볼륨을 연결하자 `hello.txt`가 그대로 존재.
- → **볼륨은 컨테이너 생명주기와 분리되어 데이터를 영속 보관**한다.

## 10. 이미지 목록 확인
```powershell
PS C:\...\-1> docker images
IMAGE                        ID             DISK USAGE   CONTENT SIZE
docker-practice-web:latest   d77f78cf66c1        241MB         63.9MB
hello-world:latest           c567b231f656       25.9kB         9.49kB
my-first-image:latest        a08cef289466        159MB         42.1MB
my-nginx-page:latest         0278aa90d5e2        241MB         63.9MB
my-web:latest                d411cd3f0fc1        241MB         63.9MB
nginx:latest                 5ab5b0b01097        243MB         66.8MB
ubuntu:latest                6a06111c3b0a        163MB         45.9MB
```

> ✅ 직접 빌드한 이미지(`my-*`, `docker-practice-web`)와 pull 받은 공식 이미지
> (`nginx`, `ubuntu`, `hello-world`)가 함께 관리되는 것을 확인.

## 11. Git 설정 · 연동

### 사용자 정보 설정
```powershell
git config --global user.name "본인이름"
git config --global user.email "본인아이디@example.com"
```

### 설정 확인
```powershell
git config --list
```
출력 예시 (개인정보는 가림 처리):
```
user.name=홍길동
user.email=****@****.com
core.repositoryformatversion=0
...
```

## 12. 트러블슈팅 기록

### 트러블슈팅 1
- **증상**: `docker run` 실행 시 `requires at least 1 argument` 에러
- **원인**: 실행할 이미지 이름을 빠뜨리고 `docker run` 만 입력함
- **해결**: 이미지 이름까지 포함해 `docker run -d -p 8080:80 --name web my-web` 로 재실행
- **참고**: 같은 이름의 컨테이너가 남아 있으면 `docker rm -f web` 로 정리 후 재실행

### 트러블슈팅 2
- **증상**: `re renamed.txt` 입력 시 `'re' 용어가 ... 인식되지 않습니다` 에러
- **원인**: 삭제 명령 `rm`을 `re`로 잘못 입력함 (오타)
- **해결**: 올바른 명령 `rm renamed.txt`로 재실행하여 삭제 성공
- **교훈**: PowerShell은 모르는 명령어를 CommandNotFoundException으로 알려줌