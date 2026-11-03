# -1
코디세이 1-1 연습

# 기본 명령어
- pwd: 현 위치
- ls: 목록
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
- docker ps: 실행 중인 컨테이너 
- docker run -d: 백그라운드로 컨테이너 실행
- docker logs <이름>: 컨테이너 기록 보기(문제 생기면 여기서 원인 찾음)
- docker stats --no-stream: 자원 사용량 1회 확인
- docker images: 이미지 목록

# 개발 워크스테이션 구축

## 프로젝트 개요
개발 환경(PowerShell / Docker / Git)을 설치하고
GitHub 저장소를 연결하여 워크스테이션을 구축하는 미션입니다.

## 실행 환경
- **OS**: Windows 11
- **쉘(Shell)**: PowerShell
- **Git 버전**: 2.56.0
- **Docker 버전**: 29.9.2
- **Node 버전**: 26.13.0