# DockerPra

도커컴포트 컨테이너 설치 명령어
docker-compose up[설치 및 실행]

도커컴포트 컨테이너 삭제 명령어
docker-compose down[정지 및 삭제]

도커 이미지 저장
docker save -o duplexing-nginx cms-web

도커 이미지 로드
docker load -i duplexing-nginx

도커 이미지 별 설명
duplexing-nginx: nginx_upstream_check_module 모듈 포함 컴파일 톰캣1과 톰캣2 로드밸런싱
custom-tomcat.tar: 톰캣 1과 톰캣2의 세션 클러스터링 설정
nginx-vod: nginx-vod-module.git 모듈 포함 컴파일 nginx vod 스트리밍 용
[사용 URL ex: http://example.com/hls/videos/big_buck_bunny_600k.mp4/index.m3u8]

cms-service[톰캣]에는 webapps에 컴파일된 소스 넣기[server.xml에 cis-web으로 소스 폴더명을 지정했음]
cms-web[nginx]에는 source에 컴파일된 소스 넣기[nginx.conf에 source으로 소스 폴더명을 지정했음]
=> Dockerfile에서 마운트 속성있음
