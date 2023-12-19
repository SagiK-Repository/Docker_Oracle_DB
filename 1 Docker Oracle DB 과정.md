# Docker Oracle DB 과정

<br>

# 목차
- [ ] 1. Docker Oracle DB 구성하기
- [ ] 2. script 구성하기
- [ ] 3. Script 활용한 Docker Oracle DB 구성하기

--- 

# 1. Docker Oracle DB 구성하기

- Oracle DB Container 사이트 : https://container-registry.oracle.com/ords/f?p=113:10::::::
- Oracle DB -> Enterprise 접속  
  ![image](https://github.com/SagiK-Repository/Docker_Oracle_DB/assets/66783849/fa4c50db-5d24-4373-842d-068586ab47e5)  
  - 키워드 `container-registry.oracle.com/database/enterprise:21.3.0.0`를 통해 docker 실행 가능 함을 확인합니다.

<br>

### 사용 방법

```
docker run -d --name <컨테이너_이름> \
 -p <호스트_포트>:1521 -p <호스트_포트>:5500 \
 -e ORACLE_SID=<사용할_SID> \
 -e ORACLE_PDB=<PDB_이름> \
 -e ORACLE_PWD=<데이터베이스_비밀번호> \
 -e INIT_SGA_SIZE=<SGA_메모리_MB> \
 -e INIT_PGA_SIZE=<PGA_메모리_MB> \
 -e ORACLE_EDITION=<데이터베이스_에디션> \
 -e ORACLE_CHARACTERSET=<문자_셋> \
 -e ENABLE_ARCHIVELOG=true \
 -v [<호스트_마운트_포인트>:]/opt/oracle/oradata \
container-registry.oracle.com/database/enterprise:21.3.0.0

파라미터:
 --name:                 컨테이너의 이름 (기본값: 자동 생성)
 -p:                     호스트 포트와 컨테이너 포트의 포트 매핑.
                         1521 (Oracle Listener), 5500 (OEM Express) 두 개의 포트가 노출됩니다.
 -e ORACLE_SID:          사용할 Oracle Database SID (기본값: ORCLCDB)
 -e ORACLE_PDB:          사용할 Oracle Database PDB 이름 (기본값: ORCLPDB1)
 -e ORACLE_PWD:          Oracle Database SYS, SYSTEM 및 PDBADMIN 비밀번호 (기본값: 자동 생성)
 -e INIT_SGA_SIZE:       모든 SGA 구성 요소에 사용할 총 메모리 (선택 사항)
 -e INIT_PGA_SIZE:       인스턴스에 연결된 모든 서버 프로세스에 사용할 대상 집계 PGA 메모리 (선택 사항)
 -e ORACLE_EDITION:      Oracle Database 에디션 (enterprise/standard, 기본값: enterprise)
 -e ORACLE_CHARACTERSET: 데이터베이스 생성 시 사용할 문자 셋 (기본값: AL32UTF8)
 -e ENABLE_ARCHIVELOG:   데이터베이스 생성 시 아카이브 로그 모드를 활성화할지 여부 (기본값: false). 19.3 이상에서 지원됩니다.
 -v /opt/oracle/oradata  데이터베이스에 사용할 데이터 볼륨. 컨테이너 내부의 Unix "oracle" (uid: 54321) 사용자가 쓰기 가능해야 합니다.
                         지정하지 않으면 컨테이너가 재생성될 때 데이터베이스가 유지되지 않습니다.
 -v /opt/oracle/scripts/startup | /docker-entrypoint-initdb.d/startup
                         선택 사항: 데이터베이스 시작 후 실행할 사용자 정의 스크립트가 포함된 볼륨.
                         자세한 내용은 "설정 후 및 시작 시 스크립트 실행" 섹션을 참조하세요.
 -v /opt/oracle/scripts/setup | /docker-entrypoint-initdb.d/setup
                         선택 사항: 데이터베이스 설정 후 실행할 사용자 정의 스크립트가 포함된 볼륨.
                         자세한 내용은 "설정 후 및 시작 시 스크립트 실행" 섹션을 참조하세요.
```

<br>

### 활용

- 다음과 같이 Oracle을 띄웁니다.
```bash
docker run -d -p 1521:1521 --name oracle_db \
-e ORACLE_SID=ORCLCDB \
-e ORACLE_PDB=ORCLPDB1 \
-e ORACLE_PWD=your_password \
container-registry.oracle.com/database/enterprise:21.3.0.0
```
