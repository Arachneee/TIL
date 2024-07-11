docker version : 버전확인
docker info : 도커 정보 확인
docker rm -f $(docker ps -aq) : 실행중인 컨테이너 모두 삭제
docker ps : 컨테이너 목록 조회
docker run : 컨테이너 실행
docker run -p 80:80 --name hellonginx nginx : nginx(웹 서버) 실행