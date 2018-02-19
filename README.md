# Naivechain

> 200줄의 코드로 구현한 블록체인

## Start with Docker

- 테스트 환경: Ubuntu Server 14.04 LTS (AWS EC2)

### Prerequisites

- Docker Engine
- Docker Compose

### Install Docker Engine

```sh
# 패키지 업데이트
$ sudo apt-get update
# 필요한 패키지 설치
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
# Docker GPG Key 추가
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
# Docker stable repository 추가
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && sudo apt-get update
## Docker CE(community edition) 설치
$ sudo apt-get install docker-ce
```

### Install Docker Compose

```sh
# docker-compose 설치
$ sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
# 실행권한 부여
$ sudo chmod +x /usr/local/bin/docker-compose
```

### Run Naivechain Nodes

```sh
# 3개의 노드를 실행/연결한다.
$ sudo docker-compose up -d
Starting naivechain_node1_1 ... done
Starting naivechain_node2_1 ... done
Starting naivechain_node3_1 ... done
...
```

## Start with NPM

### Prerequisites

- npm
- node
- (optional) nvm

### Install Module

```sh
# package.json에 정의된 의존성 모듈 설치
$ npm install
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN naivechain@1.0.0 No repository field.
npm WARN naivechain@1.0.0 No license field.
```

### Run Naivechain Nodes

- Node #1

```sh
# 첫 번째 노드 실행
$ HTTP_PORT=3001 P2P_PORT=6001 npm start

> naivechain@1.0.0 start /home/ubuntu/app/naivechain
> node main.js

listening websocket p2p port on: 6001
Listening http on port: 3001
```

- Node #2

```sh
# 두 번째 노드 실행
$ HTTP_PORT=3002 P2P_PORT=6002 PEERS=ws://localhost:6001 npm start

> naivechain@1.0.0 start /home/ubuntu/app/naivechain
> node main.js

listening websocket p2p port on: 6002
Listening http on port: 3002
Received message{"type":0}
Received message{"type":2,"data":"[{\"index\":0,\"previousHash\":\"0\",\"timestamp\":1465154705,\"data\":\"my genesis block!!\",\"hash\":\"816534932c2b7154836da6afc367695e6337db8a921823784c14378abed4f7d7\"}]"}
```

## API

### 현재 블록 확인

```sh
$ curl http://localhost:3001/blocks
[{"index":0,"previousHash":"0","timestamp":1465154705,"data":"my genesis block!!","hash":"816534932c2b7154836da6afc367695e6337db8a921823784c14378abed4f7d7"}]
```

### 블록 생성

```sh
$ curl -H "Content-type:application/json" --data '{"data" : "블럭 생성"}' http://localhost:3001/mineBlock
```

## References

- [Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
- [Install Docker Compose](https://docs.docker.com/compose/install/)
