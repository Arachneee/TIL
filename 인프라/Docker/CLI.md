docker version : 버전확인
docker info : 도커 정보 확인
docker rm -f $(docker ps -aq) : 실행중인 컨테이너 모두 삭제
docker ps : 실행중인 컨테이너 목록 조회
docker run {이미지명}: 컨테이너 실행
	--name {컨테이너 명}: 이름 지정
	-d : 백그라운드 실행
	-p {포트}
	{실행 명령} : 메타데이터의 cmd 덮어 쓰기
	--env KEY+VALUE 이미지명 : 메타데이터의 env 덮어쓰기
	
docker image ls : 이미지 목록 조회
docker image inspect {이미지명} : 이미지의 세부 정보 조회
docker container inspect {컨테이너명} : 컨테이너의 세부 정보 조회
docker pull {} : 이미지 저장