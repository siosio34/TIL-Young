# Docker Guides 정리

### Dockerfile
```
- 컨테이너 내의 환경을 정의
- 이미지에 태그다는건 필수는 아니지만 권장된다.
	- docker tag image username/repository:tag
- docker build -t name (현재 경로에 있는 Dokcerfile의 내용을 읽고 name 이라는 이름으로 image를 생성한다.)
```

### services
```
- 실행환경 내에서 컨테이너다.
- docker-compose.yml 파일 내에 어떤 포트를 사용할 것인지, 몇개의 컨테이너를 돌릴 것인지 필요한 메모리양이 얼만지 등을 정의한다.
```

##### docker-compose.yml 예시
```yaml
version: "3"
services:
	web:
	image: username/repo:tag
	deploy:
		replicas: 5
		resources:
			limits:
				cpus: "0.1"
				memory: 50M
		restart_policy:
			condition: on-failure
	ports:
		- "4000:80"
	networks:
		- webnet
networks:
	webnet
	
- host에서 4000포트에서 온 데이터 내용은 80번 보트랑 이어짐
- webnet은 로드 밸런싱을 위한 네트워크 설정
```

### docker swarm
```
- 2377 port(docker swarm) 2376 port(docker demon port)니 에러를 유발할수 있는 이 두포트는 사용하지 않도록하자.
```

### docker swarm 을 이용한 로드밸런싱
```
- docker swarm init(이거 안치면 swarm manager 노드로 인정을 안해줌.)
- docker start deploy -c docker-compose.yml app_name
- 저 명령어를 친뒤에 docker service ls 로 확인
- docker stack rm app_name(앱을 서비스위에서 내림)
- docker swarm leave --force(swarm을 종료시킴)
```
