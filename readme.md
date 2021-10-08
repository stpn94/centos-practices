# centos-practices

원본은 블로그에
## Linux 기초 모든 것(간략 정리) https://ok-vamos.tistory.com/10

# 목차

-   **[리눅스 기초](#no_1)**
-   **[명령어](#no_2)**
-   **[추가설치 프로그램](#no_3)**
-   **[콘솔과 터미널의 차이](#no_4)**
-   **[서버 시간 동기화](#no_5)**
-   **[vi 편집기 명령어](#no_6)**
-   **[c 컴파일 하기](#no_7)**
-   **[접근 권한](#no_8)**
-   **[Unix directory](#no_9)**
-   **[tar, gzip](#no_10)**
-   **[vi editor](#no_11)**
-   **[네트워크](#no_12)**
-   **[git, tomcat, java install](#no_13)**
-   **[자바 다운로드(리눅스)](#no_14)**
-   **[git 다운로드(리눅스)](#no_15)**
-   **[tomcat 다운로드(리눅스)](#no_16)**
-   **[maven 다운로드(리눅스)](#no_17)**
-   **[mariaDB(리눅스) 다운](#no_18)**
-   **[Jenkins(리눅스) 다운](#no_19)**

### #1. 리눅스 기초

개발 환경,  
Desktop -> Oracle VM, CentOS7

Red hat 패키지 명, rpl  
Window는 msi

-   직접 소스를 받아서 컴파일해서 설치하는 이유  
    \*경로나 파일을 직접 관리하기 위해서. 내 프로그램을 직접 관리하고 사용하기 위해서임  
    yum 등을 설치해도 되지만, 설정 파일에 미리 설정된 세팅에 맞게 설치되므로, 직접 관리하고 정하기 위해서  
    java, db, git, maven, apache 이런건 내가 직접 관리해야되는거니까 소스파일 직접 다운 받고,  
    다른 뭐, wget이런건 상관 없음 (유틸 도구 같은 것들)
-   파티션 나누기  
    \*머신을 설정할때 안정성을 위해서 파티션을 나눠주는게 좋다.  
    /root 는 필수적이며 /boot, /swap 으로 파티션을 나누었다. (하나의 고장이 다른 모든 것에 영향을 끼치는 것을 방지하기 위해)

### #2.명령어

> kickscar@localhost~\] $ \_
> 
> @ 앞 : 접속 계정  
> @ 뒤 : 접속한 시스템의 호스트 이름이다.  
> : 뒤 : 현재 위치(경로이다) 틸드 문자(~)는 접속 계정의 홈 디렉토리(/home/kickscar)의 일종의 약칭이다.  
> $ : 프롬프트 이다. 뒤에 커서가 깜빡 거리면서 명령어를 입력과 실행(엔터)를 기다리고 있다.

-   기본 명령어
    -   pwd = print work place
    -   mkdir = make directory
        -   mkdir dirname = dirname의 디렉토리 생성
        -   mkdir -p dirname/subdname = 하위디렉토리까지 생성
        -   mk -m 644 dirname = 특정 퍼미션을 갖는 디렉토리 생성
    -   ls = list
        -   ls -l = 파일들의 상세정보
        -   ls -la = hidden File까지
    -   cd = change directory
        -   cd~ = 어느 곳이든지 홈 디렉토리로 바로 이동합니다.
        -   cd.. = 상위 디렉토리로
        -   cd/dir = 절대경로 dir로 이동할 경우 사용
        -   cd- = 이동하기 바로전 디렉토리 이동.
    -   touch = 용량이 0인 파일을 생성, 날짜 변경하는 명령어
        -   touch filename = filename 의 파일을 생성
        -   touch -c filename = filename의 시간을 현재시간으로 변경
        -   touch -t 200001011200 filename = filename의 시간을 날짜정보(YYYYMMDDhhmm)로 변경
        -   touch -r filename1 filename2 = 날짜정보를 같게 변경
    -   rm fname = fname을 삭제합니다.
        -   rm fname = fname을 삭제합니다.
        -   rm -f fname = fname 을 묻지 않고 삭제
        -   rm -r dir = dir을 삭제합니다.
            -   dir는 -r 옵션 없이는 삭제할 수 없습니다.
    -   redirection 은 리눅스 스트림의 방향을 조정하는 명령어 이다.
        -   명령>파일 = 명령의 결과를 파일로 저장합니다.
            -   cat fname1 fname2 > fname3 = fname1, fname2 를 출력하고 fname3 이라는 파일에 저장
        -   명령 >> 파일 = 명령의 결과를 파일에 추가합니다.
            -   car fname4 >> fname3 = fname3 에 fname4 의 내용을 추가합니다.
        -   명령 < 파일 = 파일의 데이터를 명령에 입력합니다.
            -   cat < fname1 : fname2 의 내용을 출력합니다.
        -   ex) cat<fname1 = fname1 의 내용을 출력합니다.
    -   alias = 별명 설정
        -   alias new = 'command' = command 를 실행하는 새 명령어 new 를 만듭니다.
            -   ex)alias ls='ls -l' = ls 를 실행하면 -l 옵션을 갖는 ls를 실행합니다.
        -   alias : 현재 alias 목록을 출력합니다.
            -   unalias new : new 라는 alias 를 해제 합니다.
            -   alias 설정해도 로그아웃하면 다시 초기화가 되기때문에 따로 설정 해야한다.
            -   \[root@localhost ~\]# vi .bashrc 들어가서
            -    [##_Image|kage@brNikt/btrga2bnip9/TCEMxNemJqQkjhINUDKRMk/img.jpg|alignCenter|data-origin-width="299" data-origin-height="274" data-ke-mobilestyle="widthOrigin"|alias lla='ls -la' 를 추가 해주고||_##]
            -   그리고 로그아웃했다가 로그인 하면 로그인할때 .bashrc 파일을 읽어서 alias가 영구적으로 남는다
    -   vi "TEST.sh" = TEST 스크립트 만들기(스크립트는 like a 메크로)
    -   vi는 기본적으로 명령어 모드 (좀 있다가 다시나옴)
    -   알파벳 i = 누르면 에디팅 모드(메모장)
    -   esc = 누르면 다시 명령어 모드
    -   : = 확장명령어 모드(ex명령어모드)
    -   w = 저장
    -   q = 나가기(저장할것 저장하던지 버리던지 해야함)
    -   q! = (저장할것 저장하던지 버리던지 해야함)을 무시하고 나감
    -   wq = 저장하고 나가기
    -   cat "helloWorld.sh" = helloWorld.sh 의 내용을 본다.
    -   echo $PATH
    -   ./ = 절대경로
    -   chmod 권한부여(쫌 있다가 다시 나옴)

---

-   \\ or 절대경로 => alias 없이 사용 가능
-   useradd -g whell 계정이름 = 유저를 추가하는데 wheel 그룹에 넣겠다. wheel 그룹은 루트로 전환이 가능한 그룹
-   passwd = 패스워드 변경, passwd 계정명 = 계정의 패스워드 설정
-   sudo = 루트로 변경
-   su - = 루트로 변경하기(-를 붙여야 root에 필요한 설정 파일을 함께 읽어온다. root는 생략 가능), su 계정명 = 유저로 들어가기
-   shift + insert = Window에서 복사한 클립 붙여넣기
-   set = 환경변수 보기 (shell)
-   ps = 프로세스 보기
-   yum = 업데이트 제어, 소프트웨어 설치, 업데이트 사항 확인, 패키지 관리자
-   apt = 패키지 관리
-   yum update = 업데이트 목록 확인 및 업데이트  
    yum install  
    yum clean all = 패키지 캐시 파일 삭제  
    yum list = 모든 패키지 표시  
    yum remove <패키지 명> = 패키지 삭제
-   fdisk -l = 파티션 정보(디스크 정보) 보기
-   grep -n ro /etc/profile = /etc/profile에 ro라는 단어가 있는 것을 모두 출력하라, 라인 번호를 포함해서.
-   mount = 디스크나 usb와 같은 특정 디바이스를 사용하기 위해 하드웨어와 디렉토리를 연결하는 작업
-   | = 파이프, 앞의 결과(출력)을 뒤에 전달.
-   systemctl is-enabled sshd = 서비스 등록/해제 (부팅과 함께 서비스가 실행되는 것의 설정과 해제), 이건 그 유무를 물어봄.
-   systemctl start/stop/restart = 서비스의 시작/종료/다시시작
-   useradd -D (/etc/default) = 사용자 생성 시 기본 정보 (홈, skel정보 - 스켈 디렉토리에서 유저 디렉터리로 파일 복사함, shell종류 etc..)  
    useradd username = 그룹을 별도로 지정하지 않으면 새로 그룹을 만들어 유저를 생성함  
    useradd -g users user2 = user2를 생성해서 users라는 그룹에 포함시킨다.  
    useradd -M user3 = 홈 디렉터리 없이 유저를 생성, 특수한 목적을 위해 필요한 경우.
-   userdel userID = user삭제
-   groupadd groupID = group 생성  
    groupdel = group 삭제  
    groups groupID = 어느 그룹에 속해있는지 확인.
-   passwd(root에서) = root비밀번호 변경  
    passwd userID = userID 비밀번호 설정 및 변경
-   last = 로그인, 로그아웃한 흔적들. reboot 정보들.
-   ln -s filename simbolfile = 링크 파일 생성, 윈도우의 바로가기 역할
-   make = makefile 만들어서 의존성 관계, 명령어 입력 후 실행 가능

---

touch = 파일 수정 안하고 다시 다 컴파일 하고 싶을 때( //touch \*.c)

chown -R = chown -R webmaster:wheel /home/webmaster/dowork, 사용자 바꾸기 (-r 디렉토리 밑의 모든 파일도)

cp = copy  
mv = rename, 옮기기

<파일 보기>  
cat = 스크롤 형식으로 보여줌  
more = 한 페이지씩 잡아서 보여줌  
less = more의 진화된 형, : 형태의 vi편집기와 유사, editting 기능만 제외.

<찾기>  
find /찾는위치 -name '\*log' = 파일 찾기 명령어  
whereis ls = ls명령어의 위치  
ex) ps -ef | grep sshd | grep -v grep : ps -ef 중에 sshd가 들어간 행 중에서 grep이란 글자가 포함된 행을 제외한 결과를 출력

<파이프와 리다이렉트>  
프로세스 | 프로세스 = 프로세스의 출력을 다른 프로세스의 입력으로 결과를 출력  
출력 > 파일 = 출력을 파일로 입력

> \= append역할, 변경 내용을 추가로 입력

### #3. 추가 설치 프로그램

> 직접 다 설치해서 서비스 환경을 직접 구축하는 것 <-> 클라우딩 컴퓨팅

cronie  
cron job = 정해진 시간에 프로그램을 실행하게 하는 프로그램

rdate = 원격으로 시간을 물어봐서 시간을 맞추는 것. 시간을 정확하게 맞추고자.  
\--> 보라넷에 시간이 맞추어져 있음. 매우 정확함. 걔한테 물어봐서 시간을 리턴 받고 내 시스템 시간을 설정함  
\--> 주기적으로 실행해줘야함

gcc = gnu c compile, c로 작성되있는게 많아서 설치해줘야함.  
gcc-c++ = mariaDB 같은게 c++로 되있음

make = maven이 java프로그램들 쫙 war등으로 만들어주는 빌드 툴인데, 그런것과 같은 빌드 툴임

wget = url로 zip파일 등을 다운로드 해야할 때 사용할 프로그램

cmake = c++ compile 하는거

bind-utils = nslookup이 들어있는 놈

psmisc = 명령어 pstree써보세여. 부모 관계를 포함하여 나타내줌 --> 프로세스는 ~ 부모가 있다.

ifcofig ...기본에 설치가 안되어있었... 설치합시다

### #4. 콘솔과 터미널의 차이 ?

큰 차이는 없다 ! 터미널은 다중 실행이 가능. 터미널들은 원격으로 쉘과 연결되어 실행된다.  
원격 터미널이라고 부른다.

putty/xshell(원격 터미널) 과 같은 것을 이용해 인터넷을 통해서 원격으로 쉘과 연결할 수 있다.  
서버 측에서는 데몬 서버 프로그램이 떠 있어야함.  
\--> 암호화 되어있는 연결, 통신,  
ssh(secure shell) ----- telnet은 암호화되어있지 않을 뿐 같은 거임.  
ssh client / ssh server

ps -ef 명령어 실행 후 /usr/sbin/sshd -D와 같은 것이 실행되어있는 것이 보인다면 이게 바로 서버 프로그램임.  
xshell / putty 와 같은 원격 터미널을 통해 접속 가능. 호스트 ip, 통신 포트는 22번으로 연결함.

```
     집에서 연결은 할 수 없다. 왜?
```

집에서 사용하는 ip는 공용 ip이고 현재 접속중인 ip는 사설 ip로 10, 192, 127번대 ip이다.  
공용 ip는 KT 등과 같은 곳으로부터 유동 ip 혹은 고정 ip로 비어있는 ip를 받는 것이다.(공유기 등을 통해)  
이 공유기는 네트워크를 만들고 이 네트워크를 사설 네트워크라고 부른다.

여기서, 같은 사설 ip 주소를 가지고 있는 경우에 인터넷이 나를 어떻게 찾을까.  
[https://api.ipify.org/를](https://api.ipify.org/%EB%A5%BC) 통해 보면 같은 공용 ip를 가지고 있음을 알 수 있다.  
\--> 공유기는 ARP 프로그램을 통해 거쳐서 나가면서 ip가 변경되어 공인 ip로 나갈 수 있게 바꿔준다.  
공유기는 게이트웨이 역할도 하고 있다고 할 수 있다.

### #5. 서버 시간 동기화

서버를 운영하다 보면 시간 동기화를 하지 않을 경우 시간이 조금씩 어긋나게 된다. 이를 막아주기 위해 rdate 혹은 다른 방법을 이용해서  
서버 시간을 국제 시간에 동기화 시켜 주어야 한다.  
\--> 스크립트를 작성하였다.

### #6. vi 편집기 명령어

:w = 저장  
:q = 나가기  
:q! = 강제 나가기  
/검색어 = 검색 (명령모드에서)

### #7. C 컴파일 하기

> hello.c ------\[compiler\]--------> hello.o -----\[link+library\]------->hello

> hello.py------------------------------------>interprinter(실행기)  
> hello.js ----------------------------------->interprinter(실행기)

gcc 컴파일러 사용.  
gcc -o 파일명 목적파일 --> 실행파일  
\-o로 실행파일을 지정해주지 않으면 a.out으로 컴파일되게 되어있음. 내가 만든 라이브러리와 붙이기 위해선 개별적으로 설정해야한다.  
gcc -c 파일명 명령어로 목적파일을 만들도록 컴파일하고, 라이브러리 링크 작업을 위해 gcc -o 파일명 목적파일 명령어를 입력한다.

```
  --> 실행파일을 바로 실행했을 때 실행이 되지 않는 이유
```

윈도우는 현재 위치에서 찾는 것과 달리 리눅스와 유닉스는 지정된 PATH에서 파일을 찾게 된다. 그러므로 PATH 설정을 해주던가  
경로를 입력하여 실행해주어야한다. (절대 경로 혹은 현재 위치의 상대 경로)

### #8. 접근권한

[##_Image|kage@DS58p/btrfU3VVC8d/1vBC04Q2FtuPrjoTvqR270/img.png|alignCenter|data-origin-width="774" data-origin-height="76" data-ke-mobilestyle="widthOrigin"|||_##][##_Image|kage@bMCHXi/btrfXxBKPij/bvkZVXj9b1ERu4LOfU0rVK/img.png|alignCenter|data-origin-width="774" data-origin-height="272" data-ke-mobilestyle="widthOrigin"|||_##][##_Image|kage@c1IFb3/btrfRn1Rj2L/CwDOVbf9a7V547ZnZp05U0/img.png|alignCenter|data-origin-width="828" data-origin-height="304" data-ke-mobilestyle="widthOrigin"|||_##]

rw- : 소유자 접근권한 rw- : 그룹 접근권한 r-- : 기타 사용자 접근권한

r -> 4(read)  
w -> 2(write)  
x -> 1(execute)

실행파일  
r-x => 5  
rwx => 7

일반파일  
rw- => 6  
r-- => 4

chmod 명령어를 사용하여 권한 설정, ex) chmod 700

### #9.Unix directory

/ = 최상위  
/root = root의 기본 경로  
/etc = 설정파일  
/var = 어플리케이션들이 남기는 로그들이 주로 저장된다.  
/home = user들의 기본 경로.  
/dev = device 파일들의 집합

기본적으로 프로그램 다운시 설치되는 경로  
/usr/local/bin  
/usr/local/lib == 라이브러리

-   다중 사용자 환경. 서비스와 같음  
    네트워크 보안, 트래픽 제어  
    ssh 접속으로 바로 루트로 접속 불가, 루트 접속 권한이 있는 사용자 계정으로 접속 후 전환해야한다.  
    shell 종류 : bsh, bash, ksh, zsh etc..  
    디렉터리 구조(하다보면 머리에 들어온다 ~)  
    리다이렉트 (>)
-   /dev/pts/0 --> 특수 파일, 파일이라고 생각하면 안됌. 드라이버랑 연결,드라이버를 통해서 연결되어있는 장치 파일이라생각. 캐릭터형으로 작성. 디스크랑 연결되어있는 파일(sda0,1,2...)은 블록 단위로 파일 맞음.
-   파일간의 의존성

### #10. 압축, tar(archining == 압축 없이 모아논것)

디렉터리 구조를 그대로 유지하면서 모음 tar cvf name /경로 및 모을 파일 == 아카이빙 tar xvf name == 해제

tar xvfz == 압축 해제 및 아카이빙 해제

gzip file == gzip압축 gzip -d file.gz == gzip압축해제

### #11. vi editor

sHitf + g = 맨 아래로.

"이름설정 + Y/yy = 지정된 행을 버퍼에 이름을 설정하여 저장  
"설정된 이름 + p = 이름으로 저장된 내용을 붙여넣기  
ex)"1 + Y, "1 + p

:w %.old : 백업 파일 만들기  
:!명령어 : 한줄 명령어 shell에서 실행하고 돌아오기  
:sh : shell에서 작업 후 exit하면 다시 돌아옴

```
맥 os clipboard
```

맥의 경우 clipboard를 사용하기 위해선 vimrc파일 설정을 해줘야 한다.  
홈에서 .vimrc 파일을 만들어서 vi가 사용자 설정을 읽어들일 수 있게 해주는 것이다.

vi --version | grep file을 통해 설정파일을 저장할 경로를 확인할 수 있다.

기본적으로  
set nu  
set clipboard=unnamed " use OS clipboard 를 설정하여  
clipboard 사용과 행 번호 출력을 설정하였다.  
Tmux에서도 함께 사용하기 위해선  
[https://rampart81.github.io/post/vim-clipboard-share/](https://rampart81.github.io/post/vim-clipboard-share/)  
아래의 블로그를 읽어보는 것도 좋다.  
[https://iamfreeman.tistory.com/entry/vi-vim-%ED%8E%B8%EC%A7%91%EA%B8%B0-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC-%EB%8B%A8%EC%B6%95%ED%82%A4-%EB%AA%A8%EC%9D%8C-%EB%AA%A9%EB%A1%9D](https://iamfreeman.tistory.com/entry/vi-vim-%ED%8E%B8%EC%A7%91%EA%B8%B0-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC-%EB%8B%A8%EC%B6%95%ED%82%A4-%EB%AA%A8%EC%9D%8C-%EB%AA%A9%EB%A1%9D)

### #12. 네트워크

이론

네트워크란?

> “유/무선 으로 연결되어 있는 Device들의 집합 ”

데이터 통신 방법

1\. 두 개의 상이한 두 디바이스가 물리적으로 떨어져 있는 경우, 유/무선을 통해 네트워크 에 연결되어야 한다.

2\. 연결된 두 디바이스는 전류나 전파, 빛 등의 방식으로 데이터 통신을 한다.

3\. 이 데이터는 0/1 또는 on/off의 1bit로 표현되게 된다. (byte 단위 데이터 통신)

4\. 주소( address )

```
\- 두 디바이스가  데이터 통신을 하기 위해서는 서로의 위치를 알아야 한다.

\- 이 위치를 네트워크에서는 node 라고 부른다.

\- 각 node 마다  고유의 주소를 가지고 있어야 한다.
```

5\. 데이터 통신을 할 때는 데이터 외에 어디로 보내야 하는 가 또는 누가 보내는 가 등의 정보를 담고 있어야 한다.

실습

6\. 실제, 네트워크를 통한 데이터 통신을 할 때는 **Packet** 을 사용하게 된다.

[##_Image|kage@xHeEP/btrgilO10zp/eKKL0wIcoPRLmIWixwsjAk/img.png|alignCenter|data-origin-width="504" data-origin-height="230" data-ke-mobilestyle="widthOrigin"|||_##]

OSI 7계층과 TCP / IP 4계층

\- 하드웨어, 운영체계, 접속 매체와 관계없이 동작할 수 있는 개방형 구조

\- OSI 7 계층에서 4계층으로 단순화.

[##_Image|kage@dBMMHF/btrghQWfLe6/npJVnAKkQcudRkRGfMZKJ0/img.png|alignCenter|data-origin-width="676" data-origin-height="406" data-ke-mobilestyle="widthOrigin"|||_##]

Link 계층( Link Layer )

1\. Host(호스트)간의 네트워크를 통한 데이터 통신을 위한 물리적 연결(유/무선)에 대한 표준

2\. LAN, WAN, MAN과 같은 네트워크 구성을 정의

3\. 상위 계층인 Intenet 계층에서 형성된 Packet(패킷) 을 전기신호 또는 광 신호로 바꾸어 전달하는 역할을 담당한다.

4\. 응용(Application) 개발자가 직접 접근할 수 있는 계층이 아니고 보통 네트워크 장비나 드라이버 개발자 들이 관심을

```
가지는 계층이다.
```

Internet 계층 ( Internet Layer )

1\. Link 계층을 통해 물리적으로 연결된 각 Host간의 Packet의 전달 경로를 결정한다.

2\. IP(Internet Protocol)은 인터넷 계층에 존재하는 프로토콜이다.

3\. IP 프로토콜에는 IP 주소(Address)를 부여하는 방법과 체계를 정의하고 있다.

4\. IP 프로토콜은 IP 주소를 기반으로 경로를 Routing 하는 방법을 정의하고 있다.

5\. Transport(전송) 계층과 함께 Internet에서 중요한 계층이다.

6\. 데이터가 상대방에게 안전하게 전송되는 것을 보장하지 않는다.

7\. Transport(전송) 계층이 데이터 전달에 대한 신뢰성을 책임진다는 가정하에 목적지로 Packet을 어떤 경로로 전송할 것

인가에 대한 문제만 해결하는 계층이다.

Internet 계층 ( Internet Layer )

8\. IP 주소는 다음과 같이 2종류로 나뉜다.

```
IPv4 ( Internet Protocol Version 4) : 4byte 주소체계

IPv6 ( Internet Protocol Version 6) : 16byte 주소체계
```

9\. 4Byte IP주소는 Network주소와 Host(호스트) 주소로 나뉜다.

전송 계층( Transport Layer )

1\. 하위 계층 Internet 계층의 IP가 해결한 목적지까지의 네트워크상의 경로에서 실제 데이터를 전송하는 역할을 한다.

2\. TCP와 UDP 라는 데이터의 전달을 책임지는 프로토콜이 존재한다.

3\. IP는 하나의 Packet이 전달되는 과정에만 중심을 두고 설계 되었기 때문에 여러 Packet으로 나눠져 전달되는 데이터

```
의 순서와 전송 자체는 신뢰할 수 없다.
```

4\. 데이터의 순서와 신뢰할 수 있는 데이터 전송을 보장하는 역할을 전송 계층의 프로토콜이 맡는다.

5\. TCP( Transmission Control Protocol)

```
 (1) 연결지향 프로토콜이라 데이터를 전송/수신하기 전에 소켓을 통해 양쪽 연결이 성립

 (2) 연결이 성립되면 TCP는 데이터의 손실이나 중복 없이 목적지에 확실하게 전달

 (3) 만약 이때 보낸 데이터의 일부가 유실되었다면 수신자는 발신자에게 해당 데이터의 재전송을 요청한다. 

 (4) 흔히,  TCP를  전화 통화와 비교된다.

 (5) TCP는 UDP에 비해 프로토콜이 더 복잡하고 속도도 느리다.

 (6) UDP에 비해 신뢰성 있는 데이터 전송이 가능하다는 장점 때문에 HTTP, FTP, TELNET 등 대 부분 응용계층 프로토

     콜은 전송 계층으로  TCP를 이용한다.
```

6\. UDP( User Datagram Protocol )

```
(1) UDP는 비 연결지향 프로토콜이다.

(2) 전송한 데이터가 잘 전달되었는지 확인하지 않고 단지 데이터를 보내는 것으로 자신의 임무를 다한 것으로 생각

     한다.

(3) UDP는 TCP에 비해 신뢰성이 떨어지는 프로토콜이다.

(4) 흔히,  편지를 보내는 것에 비유

(5) 음악이나 동영상의 Streaming 서비스 같은 것에 적당한 프로토콜이다.
```

응용 계층 (Application Layer)

1\. 하위 계층이 목적지가 되는 호스트에 데이터를 안전하게 전달하는 신뢰에서 응용계층에서는 응용 프로그램(프로세스)

```
들이 데이터 통신을 하게 된다.
```

2\. 응용 계층의 응용 프로그램(프로세스) 들의 데이터 통신에는 매우 다양하다.

```
       ex) 메일을 보내기(SMTP),  파일을 전송하기(FTP), 웹사이트에 접속하기(HTTP)

       각 각의 목적에 맞는 데이터 통신을 위한 응용 프로토콜이 이미 정의되어 있기도 하고

       사용자 프로토콜을 설계하여 인터넷  기반의 서비스를 개발할 수 있다.
```

3\. Socket(소켓)은 응용 계층에서 개발되는 응용 프로그램에서 하위 계층의 TCP/IP의 역할을 감추어 준다. (투명성)

4\. Socket(소켓)이라는 도구를 사용하면 응용 프로그램 간의 성격에 따라 기 설계된 응용 프로토콜을 구현한 프로그램을

개발하거나 프로토콜을 설계하고 구현하면 된다.

5\. 대부분의 네트워크 프로그래밍은 socket을사용하여 위와 같은 작업을 하는 것이라 할 수 있다.

[##_Image|kage@cieUQF/btrghPpxFC5/F4kZrnqr9soPLA9oh4kFr1/img.png|alignCenter|data-origin-width="665" data-origin-height="494" data-ke-mobilestyle="widthOrigin"|HTTP||_##]

TCP/IP 프로토콜 스택(stack, 계층)

1\. TCP/IP 프로토콜 스택은 총 4개 부분으로 나누어 진다.

2\. 네트워크상의 데이터 통신 과정을 4개의 영역으로 계층화 한 것

[##_Image|kage@0baCQ/btrgdFVgHoU/WYUfrf9RwfSWk9Ajm5S8Wk/img.png|alignCenter|data-origin-width="600" data-origin-height="134" data-ke-mobilestyle="widthOrigin"|||_##]

3\. 데이터 통신 과정을 하나의 덩치 큰 프로토콜로 해결한 것이 아니고 작게 나눠서 계층화하려는 노력의 결과이다.

4\. 왜 OSI 7계층을 모두 사용하지 않는가?

```
 \- OSI 7계층은 이론적인 면과 하드웨어 장비적인 표준을  위해 제정한 것이다.

 \- 실무에서 네트워크 프로그래밍을 할 경우 90% 이상의 위의 프로토콜 스택을 기반으로 작업

    하게 될 것이다.
```

[##_Image|kage@wpmp2/btrgcAfBPO7/ZeHpo85ikaotCHez2iGqTk/img.png|alignCenter|data-origin-width="582" data-origin-height="522" data-ke-mobilestyle="widthOrigin"|||_##]

1\. TCP/IP 프로토콜의 프로그래머 인터페이스

2\. 네트워크 프로그래밍에서 개발자에게 네트워크에 접근할 수 있는 인터페이스 제공

3\. 1986년 BSD Unix4.3 개정된 소켓 사용

4\. 프로세스 간의 통신 방식( 클라이언트 / 서버모델 )

5\. 3가지 과정으로 사용

(1) 소켓 생성(소켓 열기) int socket( int domain, int type, int protocol )

(2) 소켓을 통한 송/수신

(3) 소켓 소멸( 소켓 닫기)

domain : 소켓이 사용할 프로토콜 체계( Protocol Family )

```
\- PF\_INET : IPv4 인터넷 프로토콜 체계

\- PF\_INET6 : IPv6 인터넷 프로토콜 체계

\- PF\_LOCAL : 로컬 통신을 위한 UNIX 프로토콜  체계

\- PF\_PACKET : Low Level 소켓을 위한 프로토콜  체계

\- PF\_IPX : IPX 노벨 프로토콜  체계
```

type : 소켓의 유형

\- SOCK\_STREAM

```
     1) TCP 통신 소켓이다.

     2) stream 방식의 연결지향 소켓을 만든다.(  전화와 비슷한 연결  )

     3) 양방향  통신

     4) 바이트를 주고 받을 수 있는 가변 길이 stream

     5) 전달된 모든 데이터는  에러 없이 원격지에 도달

     6) 전달된 순서대로 수신됨

\- SOCK\_DATAGRAM

    1) UDP 통신 소켓이다.

    2) datagram 방식의 비 연결성 소켓을 만든다. ( 전보와 비슷한  비 연결 )

    3) 양방향 통신

    4) 고정길이의 메시지를 사용

    5) 신뢰성이 없다.

    6) 전달된 순서대로 수신되지 않음
```

protocol : 프로토콜 선택

```
\-  0을 세팅 하여도 충분히 원하는 소켓을 생성할 수 있음

\-  하나의 프로토콜 체계에서 데이터 전송방식이 동일한 프로토콜이 2개 이상 존재하기 때문에 마지막

   파라미터를 통해 원하는 프로토콜 정보를 조금 더 구체화한다.

1)  IPv4  인터넷 프로토콜 체계에서  연결지향형  데이터 송수신 소켓

    int sockfd = socket( PF\_INET, SOCK\_STREAM, IPPROTO\_TCP );

2)  IPv4  인터넷 프로토콜 체계에서 비 연결 지향형 데이터 송수신 소켓

   int sockfd = socket( PF\_INET, SOCK\_DGRAM, IPPROTO\_UDP );
```

OS 구조와 TCP/IP 그리고 socket의 위치

[##_Image|kage@CFMgZ/btrgcBr4eoI/FiO23tCFC5RZxia08mF4s1/img.png|alignCenter|data-origin-width="811" data-origin-height="433" data-ke-mobilestyle="widthOrigin"|||_##]

포트의 필요성

\- 실제적인 데이터 통신은 연결된 두 Host(컴퓨터)의 Process(프로그램) 사이에서 이루어 진다.

\- 여러 계층을 통해 애플리케이션 계층으로 들어온 데이터를 해당 Process에만 정확하게 전달할 필요가 있다.

\- 하나의 Host(컴퓨터)에는 여러 개의 Process(프로그램)가 각각의 소켓을 사용하여 데이터 통신을 하고 있기 때문에

TCP에서는 각 소켓을 구분할 필요가 생긴다.

\- 이 때 각각의 소켓을 구분 할 때 사용하는 것이 포트 이다.

\- 쉬운 예시

> “ 아파트(Host)에 사는 사람(Process)에게 편지(Data)를 보낼 때,  
> 동(IP Address)과 호(Port)를 봉투(Packet)에 기입해야 한다.”

1\. 포트번호는 16비트 정수를 사용한다. ( 0 - 65535 )

2\. 포트의 종류

```
(1)      1 - 255      : 잘 알려진 인터넷 서비스 포트( Well-Known Port)

(2)   256 - 1023    : 그 밖의 인터넷 서비스

(3) 1024 - 4999    :  시스템 예약

(4) 5000 - 65535  :  사용자 사용
```

\[참고\]

[http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml](http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)

3\. 포트의 중복은 불가능하다.

4\. 하지만, 같은 UDP 포트와 TCP 포트는 중복하여 사용할 수 있다.

리눅스 실습

ping : 명령을 이용하면 다름 시스템의 네트워크가 현재 동작 중인지 알 수가 있다

사용법 : ping \[옵션\] 호스트

옵션

\-s : 패킷 사이즈를 지정한다.

\-q : 종합 결과만 보여준다.

\-i : 지연시간을 설정한다.

\-c : 보낼 패킷 수를 지정해 준다.

[##_Image|kage@ElnsZ/btrgihsg8pz/Qe2qkmzwm5YkEag2ZW1bw1/img.png|alignCenter|data-origin-width="856" data-origin-height="176" data-ke-mobilestyle="widthOrigin"|패킷 횟수를 지정해서 보낼 수도 있다 .||_##][##_Image|kage@KCKov/btrgine0O9A/DBpE68ccwL0fACBPLOWE70/img.png|alignCenter|data-origin-width="857" data-origin-height="175" data-ke-mobilestyle="widthOrigin"|보낼 패킷의 크기를 지정할 수 있다.||_##]

ping 명령어는 상대 호스트 또는 자신이 정상적으로 네트워크 작동을 하는 지 확인하는 데 아주 유용하게 쓰인다. 하지만 과도하게 사용하면 서버에 부담을 줄 수 있다.

외부의 과도한 ping을 막기 위해 ICMP echo를 ignore 시킨다.

[##_Image|kage@cq7nGY/btrgjyG2qqr/vAwX4c7G0L2IxVuhC5Hsr1/img.png|alignCenter|data-origin-width="857" data-origin-height="70" data-ke-mobilestyle="widthOrigin"|ping 응답 설정 여부 확인||_##][##_Image|kage@byUFIu/btrgjEN71s8/n3OWm8G3PdewMmKCIR7OWK/img.png|alignCenter|data-origin-width="857" data-origin-height="153" data-ke-mobilestyle="widthOrigin"|ping 응답을 막는 설정하기 위해 #vi /etc/sysctl.conf를 열고 다음을 추가 한다.&nbsp; &nbsp;다음 외부에서 ping을 시도해서 테스트 한다.||_##]

nslookup

nslookup 은 도메인 네임서버에 질의를 할 수 있는 명령어 이다. 도메인 이름의 호스트의 IP주소를 검색할 수 있고 네임서버가 올바르게 작동하는 지 확인 할 수도 있다.

사용법 : nslookup \[도메인\]

도메인을 입력하지 않으면 대화형으로 프로그램이 작동한다.

[##_Image|kage@Ch5TB/btrghQBZe91/6oUyW0UTHzvnGSwCzv9vGk/img.png|alignCenter|data-origin-width="856" data-origin-height="229" data-ke-mobilestyle="widthOrigin"|한 개의 도메인만 질의할 때 비대화형 방식으로 질의가 가능하다.||_##][##_Image|kage@m7cjr/btrgck4BWCb/d5pW37wmptRotEGhKPat7k/img.png|alignCenter|data-origin-width="856" data-origin-height="427" data-ke-mobilestyle="widthOrigin"|대화형 방식으로 여러 도메인을 질의 할 수 있다.||_##]

hostname

호스트네임을 화면에 출력하고, 호스트네임을 변경할 수 있다.

[##_Image|kage@SA8PY/btrgkU4g5lC/XP0k8ePKHa1dV8vC5m7K80/img.png|alignCenter|data-origin-width="856" data-origin-height="78" data-ke-mobilestyle="widthOrigin"|||_##][##_Image|kage@byxEDi/btrgiaNKmb3/3yA5qrPOdhGgH2Cqte4qE1/img.png|alignCenter|data-origin-width="856" data-origin-height="40" data-ke-mobilestyle="widthOrigin"|호스트 명을 변경해 보자. 비교적 간단하게 바꿀 수 있다. /etc/hostname 파일을 vi 에디터로 열고 다음과 같이 수정한다.||_##][##_Image|kage@xZSOx/btrgi2aCm3p/746G3RMffAwYgrMK8WUcf0/img.png|alignCenter|data-origin-width="856" data-origin-height="100" data-ke-mobilestyle="widthOrigin"|저장하고 반영하기 위해 재부팅 한다.||_##]

netstat : 네트워크 연결, 라우팅 테이블, 네트워크 장치의 통계정보 등 네트워크에 관련된 여러가지 정보를 확인할 수 있다.

사용법 :netstat \[옵션\]

옵션

\-a : 연결된 모든 소켓을 출력한다.

\-n : 호스트, 포트등의 정보를 이름대신 숫자로 표시한다.

\-p : 소켓을 열고 있는 프로세스의 아이디(PID) 를 출력한다.

\-r : 라우팅 테이블을 출력한다.

\-t : TCP 연결에 대한 소켓을 출력한다.

\-u : UDP 연결에 대한 소켓을 출력한다.

[##_Image|kage@XEtyi/btrgjFzthIN/9TeWLTDnD4qDRakAnyQ3p1/img.png|alignCenter|data-origin-width="856" data-origin-height="130" data-ke-mobilestyle="widthOrigin"|현재 시스템의 라우팅 테이블을 확인해 보자. &nbsp;||_##][##_Image|kage@miTwj/btrgh9gZp68/qYRq8ZYhMPEKWQFzlD0KPK/img.png|alignCenter|data-origin-width="856" data-origin-height="131" data-ke-mobilestyle="widthOrigin"|현재 열려 있는 TCP 포트 정보를 출력해보자||_##][##_Image|kage@dmt340/btrgjE1DF5A/irJsc3gXa0q1QW81HFyFEK/img.png|alignCenter|data-origin-width="856" data-origin-height="130" data-ke-mobilestyle="widthOrigin"|현재 열려 있는 TCP 포트의 프로세스까지 출력해 보자||_##]

ifconfig : 네트워크 인터페이스를 설정하고, 현재 네트워크 인터페이스의 정보를 알아보는 명령어이다.

대부분 네트워크 서정을 확인하는 명령어로 많이 사용된다.

사용법 : ifconfig \[옵션\]

[##_Image|kage@bYmRab/btrgjFsIFOG/qI6Kmy8IQD0qmcbvbhUnkk/img.png|alignCenter|data-origin-width="856" data-origin-height="335" data-ke-mobilestyle="widthOrigin"|전체 네트워크 인터페이스의 설정을 확인해 보자 &nbsp;||_##][##_Image|kage@bfHwyt/btrgczOyDQJ/XdvnRZKsKolC3o1Mcea821/img.png|alignCenter|data-origin-width="856" data-origin-height="161" data-ke-mobilestyle="widthOrigin"|인터페이스(interface)는 NIC(Network Interface Card)를 말하며 보통 랜카드 이더넷 카드라고 부른다. 특정 네트워크 인터페이스에 대한 정보만 출력할 수 있다.||_##][##_Image|kage@bhqnbV/btrginF6CGX/N0pGHku4rEdkUqNMEHK4Tk/img.png|alignCenter|data-origin-width="473" data-origin-height="321" data-ke-mobilestyle="widthOrigin"|네트워크를 중지하자.||_##][##_Image|kage@4zlhW/btrgimUM5AM/m7DXanuUHKWJFHB5rORTj0/img.png|alignCenter|data-origin-width="650" data-origin-height="442" data-ke-mobilestyle="widthOrigin"|네트워크 인터페이스 enp0s3 에 IP address 를 192.168.1.254 바꾸고 다시 시작해 보자||_##]

```
DNS 서버 변경하기
```

/etc/resolv.conf -> DNS 주소 변경하기

```
ping, ICMP 열기
```

/etc/sysctl.conf  
new.ipv4.icmp\_echo\_ignore\_all=0 입력

```
/etc/hosts
```

ip주소와 별칭 매칭하기  
주소 별명  
dns name 과 hostname 은 다른것

```
netstat -r/t
```

특정 포트가 열려있는지 확인하기 좋음  
ex) nestat -a | grep ssh => listen 을 보면 어디로 들어오는지 확인 가능  
netstat -a | grep portnum  
netstat -anpt | grep sshd ====>>>>

```
네트워크 카드 다운
```

ifconfig enp0s3 down -> 서버에서 다시 열어줘야함  
장치명 확인  
**\*\* /etc/sysconfig/network-script \*\*\*\***

서버에서 다시 up

```
고정 ip 설정하기
```

/etc/sysconfig/network-scripts  
ifcfg-enp0s3 파일 수정

ifconfig

inet 10.0.2.15 netmask 255.255.255.0

게이트웨이

netstat -r

10.0.2.2

nslookup

[www.douzone.com](http://www.douzone.com)

```
    입력하기 
    BOOTPROTO => "static"
IPADDR="192.168.80.116"
GATEWAY="192.168.80.254"
NETMASK="255.255.255.0"
DNS1="168.126.63.1"

/etc/resol::v.conf
nameserver -> 168.126.63.1

/etc/hosts 
/etc/hostname

***** systemctl restart ****
```

### #13. git, tomcat, java install

메모장 참고,

[https://bamdule.tistory.com/56](https://bamdule.tistory.com/56)  
참고

```
    05.13
```

리눅스 내부 구조  
프로세스 자료 구조  
/proc 는 특수 파일로서 프로세스 정보를 받아오는 것임.  
ps 명령, ps -aux / -ef 자주 사용.

maven 설치

```
export란 ? **
```

shell의 env에서 프로그램들이 프로그램을 사용하기 위해서 위치를 찾아서 상속?할 수 있게 해주는.  
찾아갈 수 있게 보내주는 것.

### #14. JAVA 다운

일반 웹에서 링크 걸려있는 다운로드  
다운로드 링크 복사  
wget (shift+insert == 붙여넣기)

\*\*로컬에서 움직이고 싶을땐 lcd

```
    1. JDK 다운 (oracle의 경우, wget이 안되도록 되어있음)
```

jdk-8u291-linux-x64.tar.gz 다운(java 8)(로컬에)

```
    2. ftp 이용
```

파일 설치 위치로 xshell을 이용하여 이동  
\-- sftp userID@IP  
\-- 파일명 복사 (ctrl + insert)  
\-- put 파일명(shitf + insert)

```
    3. 올라와있는거 확인후 해제, root홈으로 

    4. 파일 위치 정하기
```

/usr/local/douzone/java(java,git,mariadb)

```
    5. 파일을 지정된 디렉터리로 옮기기 (설치)
    6. 링크 파일 생성하기 (버전 관리)
```

ln -s /usr/local/douzone/java1.8 /usr/local/douzone/java

버전확인  
/usr/local/douzone/java/jdk1.8.0\_291/bin/java -version

```
    7.설정
```

vi /etc/profile 에 아래 정보 입력  
\# java  
export JAVA\_HOME=/usr/local/douzone/java/jdk1.8.0\_291  
export CLASSPATH=JAVA\_HOME/lib/tools.jar  
export PATH=$PATH:$JAVA\_HOME/bin

```
    8. 현재 shell에 환경에 적용하기
```

source /etc/profile

```
    9. 파일 작성하고 컴파일 하기
```

.java 로 코드 작성하고  
javac 로 컴파일  
java -cp . 파일경로/파일명(.클래스 빼고)  
완료!

### #15. GIT(리눅스) 다운

의존성 라이브러리

-   yum install gettext-devel
-   yum install openssl-devel
-   yum install zlib-devel
-   yum install perl-devel
-   yum install asciidoc
-   yum install xmlto
-   yum install expat-devel
-   yum install curl-devel
-   다운로드
-   wget [https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz](https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz)
-   압축 풀기
-   tar xvfz git-2.9.5.tar.gz

4.소스 디렉토리

-   cd git-2.9.5
-   pwd
-   configure

5.  ./configure --prefix=/usr/local/douzone/git
6.  빌드
7.  make all doc html info
8.  설치
9.  make install install-doc install-html install-info
10.  설정(/etc/profile)

# git

export PATH=/usr/local/douzone/git/bin:$PATH

\[root@localhost ~\]# source /etc/profile  
\[root@localhost ~\]# echo $PATH

9.  git 환경 설정

\# git config --global user.name "gitID"  
\# git config --global user.email "[gitID@gmail.com](mailto:gitID@gmail.com)"

10.  git 사용하기

mkdir centos-practices

cd centos-practices

git init

git add -A

git commit -m "first commit"

git remote add origin [https://github.com/stpn94/centos-practices.git](https://github.com/douzone-busan-bitacademy/centos-practices.git)

git push -u origin master

\================

git add -A

git commit -m "...."

git push

\=========================================================

git clone [https://github.com/stpn94/javastudy.git](https://github.com/douzone-busan-bitacademy/javastudy.git)

cd javastudy

mvn clean package

### #16. TOMCAT(리눅스) 다운

-   작업은 /root
-   tomcat8 다운로드
-   wget [https://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.5.71/bin/apache-tomcat-8.5.71.tar.gz](https://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.5.71/bin/apache-tomcat-8.5.71.tar.gz)
-   압축 풀기
-   tar xvfz apache-tomcat-8.5.65.tar.gz
-   설치
-   ln -s /usr/local/douzone/tomcat8.5 /usr/local/douzone/tomcat
-   mv apache-tomcat-8.5.65 /usr/local/douzone/tomcat8.5
-   설정(/etc/profile, 생략)
-   포트 확인8080 open 확인
-   vi /usr/local/douzone/tomcat/conf/server.xml
-   실행ps -ef | grep java/8080  
    8080-->8088(8088로 임의로 지정했다.)
-   vi /usr/local/douzone/tomcat/conf/server.xml
-   ps -ef | grep tomcat
-   /usr/local/douzone/tomcat/bin/catalina.sh start
-   브라우저로 접근 하기  
    [http://127.0.0.1:8088](http://127.0.0.1:8088)
-   중지 시키기
-   /usr/local/douzone/tomcat/bin/catalina.sh stop
-   서비스 등록 하기  
    /usr/lib/systemd/system/tomcat.service 파일 생성
-   systemctl enable tomcat

tomcat 서비스 실행/중지/재실행

-   systemctl restart tomcat
-   systemctl stop tomcat
-   systemctl start tomcat

10.5. tomcat manager 설정

1) tomcat-users.xml 설정  
넣기  
\----------------------------------------------------------

\[Unit\]  
Description=tomcat8  
After=network.target syslog.target

\[Service\]  
Type=forking

Environment=JAVA\_HOME=/usr/local/douzone/java  
User=root  
Group=root

ExecStart=/usr/local/douzone/tomcat/bin/startup.sh  
ExecStop=/usr/local/douzone/tomcat/bin/shutdown.sh

UMask=0007  
RestartSec=10  
Restart=always

\[Install\]  
WantedBy=multi-user.target

\-----------------------------------------------------------------

11.  tomcat manager 설정  
    1) tomcat-users.xml 설정
12.  vi /usr/local/douzone/tomcat/conf/tomcat-users.xml

\========================================================

. . .  
. . .

\\======================================================== 2) /usr/local/douzone/tomcat/webapps/manager/META-INF/context.xml \\======================================================== 주석 처리 하기

↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑주석처리

새로 다음내용 추가

↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓ ↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑

\========================================================

tomcat 재시작

-   systemctl start tomcat

12.  ps -ef | grep tomcat
13.  systemctl stop tomcat
14.  [http://127.0.0.1/manager](http://127.0.0.1/manager)

### #17. maven(리눅스) 다운

0.  작업 디렉토리  
    /root
1.  다운로드
2.  wget [http://mirror.apache-kr.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz](http://mirror.apache-kr.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz)
3.  wget [https://mirror.navercorp.com/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz](https://mirror.navercorp.com/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz)
4.  압축 풀기
5.  wget apache-maven-3.8.3-bin.tar.gz
6.  tar -xvf apache-maven-3.8.1-bin.tar.gz
7.  설치
8.  ln -s /usr/local/douzone/maven3.8 /usr/local/douzone/maven
9.  mv apache-maven-3.8.1 /usr/local/douzone/maven3.8

4\. 설정( vi /etc/profile)

# maven

export PATH=$PATH:/usr/local/douzone/maven/bin

마지막으로

source /etc/profile  
끝

### #18. mariaDB(리눅스) 다운

0.  작업 디렉토리
1.  /root
2.  pwd
3.  의존 라이브러리 설치  
    yum install -y gcc  
    yum install -y gcc-c++  
    yum install -y libtermcap-devel  
    yum install -y gdbm-devel  
    yum install -y zlib\*  
    yum install -y libxml\*  
    yum install -y freetype\*  
    yum install -y libpng\*  
    yum install -y flex  
    yum install -y gmp  
    yum install -y ncurses-devel  
    yum install -y cmake.x86\_64  
    yum install -y libaio  
    iconv 소스 컴파일 설치를 한다.

wget [https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.16.tar.gz](https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.16.tar.gz)  
tar xvfz libiconv-1.16.tar.gz

cd libiconv-1.16  
./configure --prefix=/usr/local  
make  
make install

2.  소스 다운로드  
    여기들어가면 원하는 버젼 받을수 있음([https://downloads.mariadb.org/mariadb/+releases/](https://downloads.mariadb.org/mariadb/+releases/))

-   wget [https://downloads.mariadb.org/interstitial/mariadb-10.1.48/source/mariadb-10.1.48.tar.gz/from/https%3A//archive.mariadb.org/](https://downloads.mariadb.org/interstitial/mariadb-10.1.48/source/mariadb-10.1.48.tar.gz/from/https%3A//archive.mariadb.org/)

(이름 바꾸기)  
mv index.html mariadb-10.1.48.tar.gz

3.  압축 풀기
4.  tar xvfz mariadb-10.1.48.tar.gz
5.  소스 이동
6.  cd mariadb-10.1.48
7.  빌드 환경 설정
8.  cmake -DCMAKE\_INSTALL\_PREFIX=/usr/local/douzone/mariadb -DMYSQL\_USER=mysql -DMYSQL\_TCP\_PORT=3306 -DMYSQL\_DATADIR=/usr/local/douzone/mariadb/data -DMYSQL\_UNIX\_ADDR=/usr/local/douzone/mariadb/tmp/mariadb.sock -DINSTALL\_SYSCONFDIR=/usr/local/douzone/mariadb/etc -DINSTALL\_SYSCONF2DIR=/usr/local/douzone/mariadb/etc/my.cnf.d -DDEFAULT\_CHARSET=utf8 -DDEFAULT\_COLLATION=utf8\_general\_ci -DWITH\_EXTRA\_CHARSETS=all -DWITH\_ARIA\_STORAGE\_ENGINE=1 -DWITH\_XTRADB\_STORAGE\_ENGINE=1 -DWITH\_ARCHIVE\_STORAGE\_ENGINE=1 -DWITH\_INNOBASE\_STORAGE\_ENGINE=1 -DWITH\_PARTITION\_STORAGE\_ENGINE=1 -DWITH\_BLACKHOLE\_STORAGE\_ENGINE=1 -DWITH\_FEDERATEDX\_STORAGE\_ENGINE=1 -DWITH\_PERFSCHEMA\_STORAGE\_ENGINE=1 -DWITH\_READLINE=1 -DWITH\_SSL=bundled -DWITH\_ZLIB=system
9.  빌드
10.  make

설치

-   pwd
-   /root

3.  cd (작업은 /root)
4.  make install
5.  계정 생성
6.  useradd -M -g mysql mysql
7.  groupadd mysql
8.  인스톨 디렉토리 /mariadb 소유자 변경
9.  chown -R mysql:mysql /usr/local/douzone/mariadb
10.  설정파일 위치 변경  
    cp -R /usr/local/douzone/mariadb/etc/my.cnf.d /etc
11.  기본(관리) 데이터베이스(mysql) 생성
12.  /usr/local/douzone/mariadb/scripts/mysql\_install\_db --user=mysql --basedir=/usr/local/douzone/mariadb --defaults-file=/usr/local/douzone/mariadb/etc/my.cnf --datadir=/usr/local/douzone/mariadb/data
13.  서버 구동
14.  /usr/local/douzone/mariadb/bin/mysqld\_safe &
15.  root 패스워드 설정
16.  /usr/local/douzone/mariadb/bin/mysqladmin -u root password '
17.  데이터베이스 접속 테스트
18.  /usr/local/douzone/mariadb/bin/mysql -u root -p
19.  path 설정(/etc/profile)export PATH=$PATH:/usr/local/douzone/mariadb/bin
20.  mysql

서비스(데몬, Daemon) 등록/시작/중지

-   systemctl start mariadb

3.  chkconfig mariadb on (centos7이상: systemctl enable mariadb)
4.  cp /usr/local/douzone/mariadb/support-files/mysql.server /etc/init.d/mariadb

### #19. Jenkins(리눅스) 다운

0.  작업 디렉토리/root
1.  pwd

0\. wget [https://get.jenkins.io/war-stable/2.303.1/jenkins.war](https://get.jenkins.io/war-stable/2.303.1/jenkins.war)

이동.

하기전에 톰켓 돌고 있느지 확인

```
   ps -ef | grep tomcat  
   systemctl start tomcat
```

이동

mv jenkins.war /usr/local/douzone/tomcat/webapps

[##_Image|kage@eMrOe2/btrgihZD2NG/1HF2NR76LbFVvR1MJd0kBK/img.png|alignCenter|data-origin-width="444" data-origin-height="31" data-ke-mobilestyle="widthOrigin"|war 파일이 들어가면 자동으로 톰캣이 작동한다||_##]

젠킨스 접속해보자

[http://127.0.0.1:8088/jenkins/](http://127.0.0.1:8088/jenkins/)

설정해둔 톰캣 주소로 들어간다.

[##_Image|kage@bLg3yK/btrgial6QWy/zjOAHckOUQktSaSKlQrrkk/img.png|alignCenter|data-origin-width="751" data-origin-height="524" width="376" height="262" data-ke-mobilestyle="widthOrigin"|||_##]

비민번호는

cd /.jenkins/secrets/initialAdminPassword

cat initialAdminPassword

하면 비밀번호 나온다.

그거 넣으면 된다.

[##_Image|kage@de8RXn/btrgbm2FjwE/l9NRynJkgqdiaf5XwPxSV1/img.png|alignCenter|data-origin-width="612" data-origin-height="443" data-ke-mobilestyle="widthOrigin"|||_##]

좀 오래 걸린다.... 기다리자

[##_Image|kage@b0SeIr/btrga1Lgaaz/y2klJMwJLz14XCs4YRF1Nk/img.png|alignCenter|data-origin-width="642" data-origin-height="464" data-ke-mobilestyle="widthOrigin"|||_##]

유저 만들기

끝
