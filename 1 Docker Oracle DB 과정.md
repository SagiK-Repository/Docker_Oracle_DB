# Docker Oracle DB 과정

<br>

# 목차
- [ ] 1. Docker Oracle DB 구성하기
- [ ] 2. script 구성하기
- [ ] 3. Script 활용한 Docker Oracle DB 구성하기

--- 

# 1. Docker Oracle DB 구성하기

### Docker images 다운로드
- 사이트 : https://github.com/oracle/docker-images/tree/main
- 위 사이트에선, Oracle DB를 docker 활용하기 위한 모든 내용이 들어 있습니다.
- oracle linux에서 제공하는 docker image를 기반으로 해서 oracle db를 구성합니다.  
  - Oracle linux 사이트 : https://github.com/oracle/oracle-linux
  - Oracle linux docker hub : https://hub.docker.com/_/oraclelinux
- oracle에서 구성한 docker image github 소스를 다운로드 받습니다.

<br>

### Docker Build
- 다운로드 받은 폴더 내부에 dockerfile이 존재합니다.
- `docker-images\OracleDatabase\SingleInstance\dockerfiles\21.3.0` 이동 (원하는 버전 선택합니다.)
- 원하는 버전 폴더 내부에 dockerfile을 찾습니다.
- `DockerFile` 내부 주석을 통해 docker build 합니다.
  - 예) `docker build -t oracle/database:21.3.0-xe -f Dockerfile.xe .`  
  - ![image](https://github.com/SagiK-Repository/Docker_Oracle_DB/assets/66783849/b99b1af2-a6d0-4c2d-baf6-8d8912637de9)
- Build 완료 확인합니다.  
  ![image](https://github.com/SagiK-Repository/Docker_Oracle_DB/assets/66783849/3aac6966-f35c-4e64-ae6c-98ca08607b83)

<br>

### docker run

- sample guide 문서를 참고합니다. (https://github.com/oracle/docker-images/tree/main/OracleDatabase/SingleInstance/samples/customdb)
- build를 진행한 image로 docker run 합니다. (예시 : oracle/database:12.2.0.1-ee)
```bash
docker run --name <container name> \
-p 1521:1521 -p 5500:5500 \
-e ORACLE_SID=<your SID> \
-e ORACLE_PDB=<your PDB name> \
-v <host mount point>:/opt/oracle/oradata
oracle/database:12.2.0.1-ee
```
```bash
# 예시
docker run --name oracletest \
 -p 1521:1521 -p 5500:5500 \
 -e ORACLE_SID=ORCLCDB \
-e ORACLE_PDB=ORCLCDB1 \
-e ORACLE_PWD=mirero \
-v D:\oracledb:/opt/oracle/oradata \
oracle/database:21.3.0-xe
```

