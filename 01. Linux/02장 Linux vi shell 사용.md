# Linux vi shell 사용

<br/>

## vi 사용법
### vi 시작과 종료
- :q: 수정한 내용이 없을 때, 종료  
- :q!: 수정한 내용을 저장하지 않고 종료  
- :wq, :wq!: 저장하고 종료  
- :w [파일명]: 작업한 내용을 파일명에 저장  
  - ex) :21, 38 w [파일명]: 21 ~ 38번 내용을 파일에 저장  

### 화면 이동
- [[: 맨 위로 이동  
- ]]: 맨 아래로 이동  
- :숫자: 숫자행으로 이동  

### 내용 삭제
#에 글자 수 지정  

- x, #x: 커서 위치의 글자 삭제  
- dw, #dw: 커서 위치의 단어 삭제  
- dd, #dd: 커서 위치의 행을 삭제. **잘라내기 효과**  

### 명령 취소
- u: 명령 취소

### 복사, 붙여넣기
- yy, #yy: 커서가 위치한 행 복사  
- P: 커서가 위치한 행의 아래쪽에 붙여넣기  
- dd, #dd: 커서 위치의 행을 삭제. 잘라내기 효과  

### 검색
- /문자열: 문자열을 아래 방향으로 검색. N을 누르면 ?문자열로 변경  
- ?문자열: 문자열을 위 방향으로 검색. N을 누르면 /문자열로 변경  
- n: 찾던 방향으로 다음 문자열 검색  
- N: 역방향으로 다음 문자열 검색  

### 바꾸기(substitution)
- :%s/문자열1/문자열2: 해당 라인에서 문자열1을 찾고 찾은 **첫 번째 대상만** 문자열2로 변경  
- :%s/문자열1/문자열2/g: 파일 전체에서 **모든** 문자열1을 찾아 문자열2로 변경(대소문자 구분). **:set ignorecase 하면 대소문자 구분 무시**  
- :%s/.\*/\L&/g: 대문자를 소문자로 변경  
- :%s/.\*/\U&/g: 소문자를 대문자로 변경

### 셸 명령
- :! 셸 명령: vi 작업을 중단하고 셸 명령 실행. vi로 돌아오려면 **enter**  
- :sh: vi 작업을 중단하고 셸 명령을 실행. vi로 돌아오려면 **exit**

<br/>

## vi 환경 설정
### vi 환경 설정 명령(set)
- :set nu: 파일 라인 표시  
- :set nonu: 파일 라인 숨김  


<br/>

## Shell 사용법
### 출력 리다이렉션
- 명령 > 파일명: 파일이 없으면 생성, 있으면 **덮어쓰기**. 기존 파일의 내용을 삭제하고 새로 결과를 저장. **set (+ | -)o noclobber: 덮어쓰기 허용/방지**  
- 명령 >> 파일명: 파일이 없으면 생성, 있으면 기존 파일의 **내용 뒤에 결과를 추가**

<br/>

## Alias, History
### alias
명령어에 별명을 지정해 **별명으로 명령어를 수행**할 수 있다.  
긴 명령어을 짧은 명령어로 만들어 사용 가능하다.  
여러 명령어를 하나의 명령어로 만들 수도 있다.

- alias: 현재 설정되어 있는 alias 출력  
- alias 별명='명령': 명령을 별명으로 설정  
  - ex) alias rm='rm -i'

지역적 설정: 프롬프트에 입력해 다른 세션에선 적용이 안 되게 하는 설정. **세션이 종료되는 순간 설정 증발**  
전역적 설정: .bashrc 또는 /etc/bashrc에 추가해 다른 세션에서도 적용되게 하는 설정. **세션이 종료돼도 유지**

지역적, 전역적 설정은 꼭 alias만 아니라 **다른 명령어들도 해당**

### history
명령 기록 출력

- !!: 바로 직전에 수행한 명령 재실행  
- !번호: 히스토리에서 해당 번호의 명령 실행  
- !문자열: 히스토리에서 해당 문자열로 시작하는 마지막 명령을 재실행  

<br/>

## 프롬프트 설정
### PS1
프롬프트 설정 변수. **프롬프트 식별**을 위해 사용  
환경 변수 PS1에 새로운 형태의 문자열 지정 ex) PS1 = ~~  
환경 변수 앞에 $를 붙이면 환경 변수가 가진 값을 사용할 수 있다. ex) echo $PS1  

프롬프트에서 PS1 = ~~ 이렇게 설정하면 **지역적 설정**  
.bash_profile 또는 /etc/profile에 설정하면 **전역적 설정**

<br/>

## 환경 설정 파일
### 환경 설정 파일
**사용자**가 로그인할 때마다 **자동으로 실행**되는 명령을 저장한 파일

### 시스템 환경 설정 파일
시스템을 사용하는 **전체 사용자의 공통 환경**을 설정하는 파일

- /etc/profile: 시스템 공통으로 적용되는 **환경 변수 설정**. PATH, HOSTNAME, ...
- /etc/bashrc: 시스템 공통으로 적용되는 **function과 alias 설정**

### 사용자 환경 설정 파일
**각 사용자의 홈 디렉터리**에 숨김 파일로 생성  
.bash관련 파일들은 **유저별 환경 변수**를 설정  
.bash_history, .bash_profile, .bashrc, .bash_logout

### 환경 설정 파일 적용하기
. 파일명 또는 source 파일명
