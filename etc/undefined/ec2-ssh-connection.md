# EC2 ssh connection 쉽게 하기

```
$ ssh -i {YOUR_KEY_PAIR_FILE.pem} {USER_NAME}@{AWS_PUBLIC_DNS_}
```

본인이 지정한 alias만 입력해서 접속하는 방식 `$ssh {alias}`

1. pem 키를 `~/.ssh` 경로에 복사한다 ( 이후 ssh 실행 시에 pem키를 자동으로 읽어서 접속을 진행함)

`cp {pem 키 위치} ~/.ssh`

2. pem 키 권한 변경

`chmod 600 ~/.ssh/{pem키 이름}`

3. `~/.ssh` 경로에 config파일 생성

`vim ~/.ssh/config`

```
Host {alias로 쓸 서비스 명칭}
    HostName {ec2 EIP 주소}
    User ec2-user
    IdentityFile ~/.ssh/{pem키 이름}
    
:wq!
```

4. config 파일에 실행권한 설정

`chmod 700 ~/.ssh/config`

5. `ssh {서비스 명칭}`
