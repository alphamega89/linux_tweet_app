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




  ----------------------------------------------
*** 원격접속 가능하도록 포트포워딩 하기..
  --원격접속할 리눅스에서 hostname -I 명령으로 아이피확인(10.0.2.15). 
  --원격접속할 윈도에서 ipconfig /all 이라는 명령으로 NIC(LAN card) 정보를 확인
  --Virtual box 가 붙은 장비의 IP(192.168.56.1)를 확인..

  Virtual box에서 가상머신 선택하고 설정 아이콘을 네트워크 탭으로.. 어댑터1에 NAT에 연결되어있는지 확인하고 고급클릭-포트포워딩 설정..
  Putty와 같은 프로그램(SSH)에서 연결 
  윈도에서 -- ssh 계정@Virtual box 가 붙은 장비의 IP 해도 연결됨 (ex. ssh hana@192.168.56.1)
  ----------------------------------------------

현재디렉토리에 a.out이라는 파일이 존재하는데 이 파일이 실행파일인 경우 이 파일을 실행하고자 하는경우 a.out 이라고 하면 이런 명령이 없다고 에러가 발생하는 경우가 있음.

경로인 경우는 a.out 이나 ./a.out 이 동일
실행을 하는 명령인 경우는 PATH에 등록된 곳에서 찾고 없으면 경로를 이용해서 찾는데 현재 디렉토리가 PATH에 추가되어있지 않다면 디렉토리를 포함해서 경로를 입력해야한다.

[hana@localhost ~]$ ls
adam  공개  다운로드  문서  바탕화면  비디오  사진  서식  음악
[hana@localhost ~]$ source .bashrc
[hana@localhost ~]$ ls
.   .bash_history  .bash_profile  .cache   .local    .viminfo  공개      문서      비디오  서식
..  .bash_logout   .bashrc        .config  .mozilla  adam      다운로드  바탕화면  사진    음악
[hana@localhost ~]$

**.bashrc 의 alias ls='ls -a' 로 변경했음..
리눅스에서는 등호양옆에 공백쓰지 않는다.

**ls 명령어로 경로를 썼을시, 파일존재여부, 파일인지 아닌지 확인가능
**파일인경우 파일명, 디렉토리인경우 경로, 존재하지 않는경우 존재하지 않다고 표시
[hana@localhost ~]$ ls /etc/hosts
/etc/hosts


[hana@localhost bin]$ vi time.sh
[hana@localhost bin]$ nano time.sh
[hana@localhost bin]$ cat time.sh
#!/bin/bash
echo -------------------------------------------------
echo 'current time is' $(date '+%Y-%m-%d:%H-%M-%S')
echo -------------------------------------------------
[hana@localhost bin]$ time.sh
-bash: /home/hana/bin/time.sh: 허가 거부
[hana@localhost bin]$ chmod 700 time.sh
[hana@localhost bin]$ time.sh
-------------------------------------------------
current time is 2024-08-01:14-29-44
-------------------------------------------------



[hana@localhost bin]$ cd ..
[hana@localhost ~]$ /bin/time.sh
-bash: /bin/time.sh: 그런 파일이나 디렉터리가 없습니다
[hana@localhost ~]$ ./bin/time.sh
-------------------------------------------------
current time is 2024-08-01:14-36-26
-------------------------------------------------



[root@localhost ~]# su - user1
[user1@localhost ~]$ vi .bash_profile
[user1@localhost ~]$ . .bash_profile
[user1@localhost ~]$ env | grep ORACLE
ORACLE_HOME=/u01/app/oracle/product/12.2.0/db_1
[user1@localhost ~]$ echo $PATH
/home/user1/.local/bin:/home/user1/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/                user1/.local/bin:/home/user1/bin:/u01/app/oracle/product/12.2.0/db_1/bin
[user1@localhost ~]$ vi sqlplus
[user1@localhost ~]$ chmod +x sqlplus
[user1@localhost ~]$ mv sqlplus /u01/app/oracle/product/12.2.0/db_1/bin/
[user1@localhost ~]$ sqlplus
DB connection.
SQL>
[user1@localhost ~]$ ls /u01/app/oracle/product/12.2.0/db_1/bin/
sqlplus
[user1@localhost ~]$ ls -l /u01/app/oracle/product/12.2.0/db_1/bin/
합계 4
-rwxr-xr-x. 1 user1 user1 35  8월  1 14:44 sqlplus
[user1@localhost ~]$ ls -l
합계 0
drwxr-xr-x. 2 user1 user1 6  8월  1 11:22 1234
[user1@localhost ~]$ cd ~
[user1@localhost ~]$ ls
1234
[user1@localhost ~]$ logout
[root@localhost ~]# logout
[hana@localhost ~]$


** 권한설정시..

 umask는 설정하지 않을 권한에 대한 기본설정값.
 파일은 실행권한이 설정되지 않고 디렉토리에만실행권한이 설정됨.

 권한설정은 설정값은 rwx rwx rwx
 현재 umask 설정은 022
 파일의 경우 666 에서 022를 빼면 되고 디렉토리는 777에서 022를 빼면 기본설정값
 파일의 경우 기본설정은 644 
 디렉토리의 경우 기본설정은 755

 설정변경하고자 할때 umask하고 설정..


 -포그라운드실행 : 작업이 종료될때까지 제어권을 가지고 있는 방식으로 일반적인 명령이 이 방식
 인터럽트를 발생시키거나 kill명령을 이용해서 강제 종료 가능

 -백그라운드실행 : 작업중이더라도 제어권을 다른곳으로 넘길 수 있도록 실행하는 방식으로 시간이 오래걸리거나 계속 작업을 수행하는 경우 사용. 명령을 수행할 때 맨 뒤에 &를 추가해주면 됨.


 작업목록 확인 : jobs
 -백그라운드 작업을전부 확인하는 명령

 CTRL + z : 포그라운드 작업을 일시 중지
 bg %작업번호 : 백그라운드 작업으로 전환
 fg %작업번호  : 포그라운드 작업으로 전환

 로그아웃을 한 후에도 작업을 백그라운드에서 계속 수행하기
 nohup 명령어 &

작업예약 
-종류 - 특정시간에 한번만 수행 : at 
      - 일정한 주기를 가지고 계쏙 수행 : crontab(쉘 프로그래밍을 하고 난 후 학습하면 효과가 뛰어남)

      - at 명령
      형식 : at [옵션][시각]
      옵션 
       l  -현재 실행대기중인 명령의 전체목록을 출력
       r 작업번호 : 작업번호에 해당하는 명령은 삭제
       m : 출력결과가 없더라도 작업이 완료되면 사용자에게 메일로 알려줌 --메일설정이 되어있어야함
       f 파일경로 : 명령어 입력대신 파일 경로에 해당하는 스크립트 파일을 수행.

       작업확인시 : ls - l /var/spool/cron/atjobs

       작업삭제 at -d 작업번호

       at 수행할 명령어 작성
       at>  CTRL + d를 누르면 작성이 종료되고 <EOT>가 자동으로 입력됨


       - crontab 
       작업을 주기적으로 수행할 수 있도록 해주는 명령
       사용자별로 설정
       형식
        crontab [-u 유저아이디][옵션][파일 경로]
       옵션
        e: 편집
        l: 목록을 출력
        r: 파일삭제

        파일작성시 주의점은 한줄에 하나의 명령만 기재되어야 함.

       시간설정을 할 때
       분(0~59) 시(0~23) 일(1~31) 월(1~12) 요일(0~6) 작업내용
       *을 설정하면 모든 시간이 됨.
       -을 이용하여 범위 설정가능
       쉼표를 이용하면 배열
       /이용하면 단계

       30 * * * * 작업: 매시간 30분마다 수행
       0,30 * * * * 작업 : 매시간 0,30마다 수행
       0, * * * 1-5 : 월화수목금 매시간(정각) 수행
       0-59/2 --2분마다 수행

       실제작업을 설정할 때는 ?.sh 파일을 만들어서 수행
       sh 파일을 만들시 권한설정에 유의해야함.

