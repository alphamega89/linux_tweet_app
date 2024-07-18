# Linux Tweet App

This is very simple NGINX website that allows a user to send a tweet. 

It's mostly used as a sample application for Docker 101 workshops. 

To use it:

Build it:
`docker build -t linux_tweet_app .`

Run it:
`docker container run --detach -p 80:80 linux_tweet_app`


# Linux

man [명령어] --명령어 사용법확인

echo $PATH  --   shell  이 명령어를 찾는 위치..

whereis []  --[] 위치확인

which --  PATH에 등록된 명령어의 위치검색

date

 tiemdatectl

uname -a  -- 시스템정보 확인..

sudo --관리자권한으로 명령실행
ex)sudo yum install httpd

su - 계정 -- 환경변수 유지하면서 다른계정전환 ( root로 권한변경하여 처리등..)
[user@localhost ~]$ su - root
암호:
[root@localhost ~]# ^C

**다시 돌아갈때..
[root@localhost ~]# su - user
[user@localhost ~]$



[user@localhost ~]$ which vi
/usr/bin/vi
[user@localhost ~]$ ls -l /bin/vi
-rwxr-xr-x. 1 root root 691  3월  1  2023 /bin/vi
[user@localhost ~]$

**사용자의 기본 쉘 확인..
[user@localhost ~]$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin


** > 결과 저장
** >> 기존파일의 내용 뒤에 결과추가

**텍스트에서 특정단어를 포함한 내용만 추출..
grep 단어 파일경로..
[user@localhost ~]$ date > out2
[user@localhost ~]$ cat out2
2024. 07. 18. (목) 15:14:40 KST
[user@localhost ~]$ ls -a >> out2
[user@localhost ~]$ cat out2
2024. 07. 18. (목) 15:14:40 KST
.
..
.bash_history
.bash_logout
.bash_profile
.bashrc
.cache
.config
.exrc
.lesshst
.local
.mozilla
.viminfo
exrc
out1
out2
sampla.txt
sample.txt
~exrc
공개
다운로드
문서
바탕화면
비디오
사진
서식
음악
[user@localhost ~]$

..




==> 3초마다 특정파일에 date 명령의 결과를 출력..
while true; do date >> today;sleep 3; done -- 포그라운드에서 무한반복되므로 시간이 흐른후    CTRL + C 로 중단시키고 확인

==> sar를 이용해서 모니터링 결과를 파일에 기록, 원격 서버에도 기록하기..
sar 2 3 > 파일 경로 ---로컬의 파일경로에 모니터링 결과저장..

sar 2 3 > 파일경로 && scp 파일경로 다른컴퓨터IP:디렉토리경로 
##systat  패키지는 유용하다..


## 덮어씀 방지 설정
[user@localhost ~]$set -o noclobber
[user@localhost ~]$ ls > out2
-bash: out2: 이미 있는 파일을 덮어쓸 수 없음

alias  설정시 주의상황..

레벨이 있는데  session level 에서 설정하면 터미널이 종료되면 자동삭제,  user level  에서 설정되면 유저에게는 계속 적용.. system level 에서 설정되면 모든유저 적용..
[root@localhost user]# ps -ef | grep sshd
root        1532       1  0 11:24 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root       37642    1532  0 13:55 ?        00:00:00 sshd: user [priv]
user       37647   37642  0 13:55 ?        00:00:00 sshd: user@pts/0
root       38532   38510  0 16:21 pts/0    00:00:00 grep --color=auto sshd
[root@localhost user]# alias csess='ps -ef | grep sshd'
[root@localhost user]# csess
root        1532       1  0 11:24 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root       37642    1532  0 13:55 ?        00:00:00 sshd: user [priv]
user       37647   37642  0 13:55 ?        00:00:00 sshd: user@pts/0
root       38534   38510  0 16:22 pts/0    00:00:00 grep --color=auto sshd


alias  등을  system 레벨로 설정하고자 하는 경우엔 .bashrc  파일에 기록해야함.  .bashrc 에 기록된 내용은 바로 적용되지 않는데, 재부팅 하거나   source .bashrc 명령어를 수행하여 처리..

rm 명령은 파일을 삭제하는 명령인데, 기본명령은 파일을 무조건 삭제하고, -i 옵션을 추가하면 삭제할 때 대화형으로 물어봄...
잘못된 삭제를 방지하기 위해  rm을 rm -i의 별명으로 사용함..

이렇게 만들때 안좋은 점은 여러파일 삭제시 너무 많이 물어보게됨..
(품질 4번서버..)


