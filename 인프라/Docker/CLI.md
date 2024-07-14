docker version : 버전확인
docker info : 도커 정보 확인
docker rm -f $(docker ps -aq) : 실행중인 컨테이너 모두 삭제
docker ps : 실행중인 컨테이너 목록 조회
	-a : 모든 상태의 컨테이너 조회(all)
	
docker run {이미지명}: 컨테이너 실행
	--name {컨테이너 명}: 이름 지정
	-d : 백그라운드 실행
	-p {HostOS의포트}:{컨테이너의포트}:포트포워딩
	{실행 명령} : 메타데이터의 cmd 덮어 쓰기
	--env KEY+VALUE 이미지명 : 메타데이터의 env 덮어쓰기
docker run -it --name {컨테이너명} {이미지명} bin/bash : 컨테이너 실행과 동시에 터미널 접속

docker image ls : 이미지 목록 조회
docker image inspect {이미지명} : 이미지의 세부 정보 조회
docker tag {기존이미지명} {추가할이미지명} : 로컬스토리지의 이미지명 추가

docker container inspect {컨테이너명} : 컨테이너의 세부 정보 조회

docker pull {} : 이미지 다운로드
docker push {이미지명} : 이미지 레지스트리에 이미지 업로드

docker commit -m {커밋명} {실행중인 컨테이너명} {생성할 이미지명} : 실행중인 컨테이너 이미지로 생성

docker create --name {컨테이너명} {경로} : 컨테이너 생성
docker start {컨테이너명} : 생성상태 컨테이너 실행
docker pause {컨테이너명} : 실행중인 컨테이너 일시정지
docker stop {컨테이너명} : 컨테이너 종료
docker restart {컨테이너명} : 컨테이너 재시작
docker logs {} : 컨테이너 로그 확인

docker build -t {이미지명} {도커파일 경로} : 도커파일을 통해 이미지 빌드
docker build -f {도커파일명} -t {이미지명} {도커파일 경로} : 도커파일명이 Dockerfile 이 아닌경우 별도 지정

docker cp {원본위치} {복사위치} : 컨테이너와 호스트 머신 간의 파일 복사
docker cp {컨테이너명}:{원본위치} {복사위치} : 컨테이너 -> 호스트 머신으로 파일 복사
docker cp {원본위치} {컨테이너명}:{복사위치} : 호스트머신 -> 컨테이너로 파일 복사

docker exec -it {컨테이너명} bin/bash : 컨테이너로 shell 접속

docker network ls : 네트워크 리스트 조회
docker network inspect {네트워크명} : 네트워크 상세 정보 조회
docker network create --driver bridge --subnet {서브넷 범위} --gateway {게이트웨이} {네트워크명} : 네트워크 생성
docker network rm {네트워크명} : 네트워크 삭제