##### report_open2
# 리눅스명령어와 vim에디터 매크로

### 1. 리눅스 명령어
 
**-1) top**
- 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)
- 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여

------------------------------------------------------------------------------
|명령어|내용|
|-----|----|
|-b|배치모드로 정보를 출력한다. 실시간 상화 대화형모드로 정보를 화면에 일렬로 출력합니다.|
|-d delay|지정한 시간의 초(delay)의 간격으로 정보를 업데이트하여 출력합니다.|
|-i idle|토글값이 off일때, idle 프로세스나 좀비 프로세스 정보를 출력하지않습니다.|
|-n num|지정한 시간(num)만큼 업데이트 정보를 출력합니다.|
|-p pid|지정한 프로세스 ID(pid)의 정보만을 출력합니다.|
|-q|시간의 간격없이 계속해서 업데이트 정보를 출력합니다.|
|-s|몇 개의 대화식 명령을 비활성화 합니다.|
|-S|누적된 정보를 출력합니다.|

------------------------------------------------------------------------------

**-2) ps**
 - 프로세스 목록 보기
 - pid등의 정보를 볼 수 있는 명령
 - process의 상태를 알고 싶을때 사용하는 명령
------------------------------------------------------------------------------
|명령어|내용|
|-----|----|
|ps -e, -A | 모든 프로세스를 보여줍니다.|
|ps -a | 세션 리더와 터미널과 연관된 프로세스들을 제외한 모든 프로세스를 보여줍니다.|
|ps -d | 세션 리더를 제외한 모든 프로세스를 보여줍니다.|
|ps -f | full format으로 세션의 정보를 표시합니다. |
|ps -ef | -e와 -f의 옵션 조합인데, 모든 프로세스를 full format으로 보여줍니다. 아래는 그 결과를 보여줍니다. UID, PID, PPID, C, STIME, TTY, TIME, CMD의 정보를 볼 수 있네요. TTY(연결 터미널)가 없으면 대부분 데몬 혹은 커널 프로세스입니다.|
|ps -u userlist | EUID 혹은 유저 이름으로 프로세스를 고릅니다. 이때 여러 uid를 줄수 있는데 ','(comma)로 구분하여 명시해줍니다. euid는 프로세스가 수행할때 갖는 유저 권한을 말합니다.|
|ps -U userlist | -u 옵션과는 동일하나 RUID가 갖는 프로세스만을 찾아냅니다. ruid는 real user id라는 것으로 실제 프로그램을 실행한 uid를 의미합니다. 이때도 쉼표로 여러 uid를 지정할 수 있습니다.|
|ps -p pidlist | 프로세스 id가 일치하는 프로세스를 출력합니다. 여러 pid들을 뽑아내고 싶다면 마찬가지로 ','(comma)로 pid를 구분하여 명시해줄 수 있습니다. 이 명령은 ps --pid pidlist와 같습니다.|
|ps --ppid pidlist | 부모 프로세스 id와 일치하는 프로세스를 출력합니다. 역시 여러 ppid를 ','(comma)로 구분가능합니다.|
|ps -t ttylist | tty와 일치하는 프로세스들을 출력해줍니다. 이 명령은 t 혹은 --tty 옵션과 같습니다. |
|ps -o format | 사용자가 지정한 format대로 출력합니다. format에 대해서는 설명이 길지만 간략하게 원하는 column만 보여준다고 기억하시면 됩니다. 예를 들어 사용자가 임의로 pid, ppid, cmd, uid 등을 표시할 수 있습니다.|
|ps aux | BSD 문법으로 실행중인 모든 프로세스를 나타냅니다. ps -aux와는 다른 옵션입니다. |
|ps -ejH | 프로세스를 트리 형태로 조금 보기 좋게 표시한다. 자식 트리면 CMD가 한칸 띄어져서 출력된다.|
+ ps -ef | grep ~~ : 원하는 프로세스 ~~ 찾기

------------------------------------------------------------------------------

**-3) jobs**
- 작업의 상태를 표시하는 명렁어이다.
- 터미널마다 job이 따로 존재한다.
- 현재 쉘 세션에서 실행시킨 백그라운드 작업의 목록이 출력되며, 각 작업에는 번호가  붙어 있어 kill명령어 뒤레 '%번호' 등으로 사용할 수 있다.
------------------------------------------------------------------------------
|명령어|내용|
|-----|----|
|Running|작업이 진행중|
|Done|작업이 완료되어 0을 반환|
|Done(code)|작업이 종료되었으며 0이 아닌 코드를 반환|
|Stopped|작업이 일시중단|
|Stopped(SIGTSTP)|SIGTSTP 시그널이 작업을 일시 중단|
|Stopped(SIGTOP)|SIGTOP 시그널이 작업을 일시중단|
|Stopped(SIGTTIN)|SIGTTIN 시그널이 작업을 일시중단|
|Stopped(SIGTTOU)|SIGTTOU 시그널이 작업을 일시중단|
------------------------------------------------------------------------------

**-4) kill**
- 프로세스 종료
- job도 종료가능
--------------------------------------------------------------------------------
|명령어|내용|
|-----|----|
|-ㅣ | 사용 가능한 시그널 목록을 출력|
|-1 | 재실행|
|-9 | 강제종료|
|-15 | 정상종료|
------------------------------------------------------------------------------

### 2. vim에디터 매크로

**순서**
+ qa : 매크로 a 시작
+ 반복할 동작 입력
+ q : 매크로 종료
+ @a : 매크로 a실행

|명령어|내용|
|-----|----|
|qa | 매크로 a 시작|
|q | 매크로 종료|
|@a | 매크로 a실행|
|@@ |방금 실행한 매크로 실행|
|10@a |매크a 10회 실행|

![과제4](https://user-images.githubusercontent.com/104884623/172055387-7ffeb265-82a1-410d-814c-f84f37a802b4.JPG)
