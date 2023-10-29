`Node`의 버전 관리를 위해 `nvm`(Bash 스크립트) 또는 `n`(Node 모듈)을 활용 할 수 있으며 두 프로젝트 모두 활성화 된 프로젝트이므로 선호에 맞게 선택 하면 된다.

### n 설치

`n`의 경우 `Node`가 설치되어 있다면 `npm`을 이용해 간단히 설치할 수 있다.

```shell
sudo npm install -g n
```

시스템 폴더의 권한을 가져오면 sudo 명령어 없이 n install을 할 수 있다.

```shell
# make cache folder (if missing) and take ownership
sudo mkdir -p /usr/local/n
sudo chown -R $(whoami) /usr/local/n
# make sure the required folders exist (safe to execute even if they already exist)
sudo mkdir -p /usr/local/bin /usr/local/lib /usr/local/include /usr/local/share
# take ownership of Node.js install destination folders
sudo chown -R $(whoami) /usr/local/bin /usr/local/lib /usr/local/include /usr/local/share
```

ls-remote 명령을 통해 설치 가능한 버전 정보를 확인 할 수 있다.

```shell
n ls-remote
```

```
Listing remote... Displaying 20 matches (use --all to see all).
21.1.0
21.0.0
20.9.0
20.8.1
20.8.0
20.7.0
20.6.1
20.6.0
20.5.1
20.5.0
20.4.0
20.3.1
20.3.0
20.2.0
20.1.0
20.0.0
19.9.0
19.8.1
19.8.0
19.7.0
```

### n을 이용한 Node 설치 방법

Node를 설치하고 싶다면,

```shell
# 특정 버전을 설치
n install 18.18.2
# 최신 버전 설치
n latest
# 안정화 버전 설치
n lts
```

버전을 선택하려면 아래 명령어를 입력하고 원하는 버전을 선택하면 된다.

```shell
n
```

```
  ο node/18.18.2
    node/20.9.0

Use up/down arrow keys to select a version, return key to install, d to delete, q to quit
```

### Trouble Shooting

기존에 nvm을 사용했을 경우 n으로 Node를 설치하더라도 nvm으로 설치한 버전이 활성화된다.

```
     copying : node/18.18.2
   installed : v18.18.2 to /usr/local/bin/node
      active : v16.20.2 at /home/jung0han/.nvm/versions/node/v16.20.2/bin/node
```

이 경우 nvm 폴더를 삭제할 경우 정상적으로 설치된 버전이 인식된다.

```shell
rm -rf ~/.nvm
```

### Reference

[`n` – Interactively Manage Your Node.js Versions](https://www.npmjs.com/package/n#n--interactively-manage-your-nodejs-versions)

[n or nvm for managing node versions](https://stackoverflow.com/questions/41666010/n-or-nvm-for-managing-node-versions-is-keeping-global-modules-for-each-version)