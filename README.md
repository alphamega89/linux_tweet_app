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




