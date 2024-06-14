# 2024.05.27
## linux
1. ln  
	ln은 하드링크, 심볼릭 링크 있음.  
	ln [원본] [링크파일] <- 하드링크  
	원본 파일이건 링크파일이건 둘다 원본같은 존재  
	ln -s [원본] [링크파일] <- 심볼릭 링크  
	윈도우의 바로가기 같은거  
	* 공통점 :  둘다 원본과 같이 움직임 링크쪽을 수정하건 원본을 수정하건 양쪽 다 수정됨.  
	* 차이점 : 하드링크는 원본과 같은거라 원본이 지워지면 본인이 원본으로서 역활을 하지만, 심볼릭 링크는 바로가기 같은거라 원본이 지워지면 연결점이 없어져서 찾을 수 없다 뜬다.  
1. find  
	find [path] [option] [action]  
	[option] 은 -name 또는 -iname를 주로 사용
		* name : 대소문자 구분
		* iname : 대소문자 구분 안함  
		* name나 iname는 정확한 이름으로 검색을 하나 ""로 감싸면 와일드카드 사용 가능
		* name옵션 안 넣고도 사용 가능 하지만 그러면 해당 검색어가 들어가는 모든것을 검색함.  
			Ex) find dir -> dir dir/a dir/b dir/a/a ... 같이 경로에 있는 모든것을 출력함
	[option]에 -type옵션도 있음 이건 어떤 타입의 파일을 찾는지를 설정(d 디랙토리 등)
1. locate  
	find와 같은 찾기이긴 한데 이건 데이터베이스를 이용하여 찾기 때문에 더 빠르다고 함.  
	대신 데이터베이스를 만들고 갱신해야하기 때문에 장단점이 있음   
	그리고 데이터베이스에 없으면 실재로는 있어도 없다 나오거나 데이터베이스가 갱신되지 못하여 없는데 데이터베이스에 있으면 있다 나오는 문제가 있음
1. which  
	which [commed]  
	명령어를 실행하는 파일의 위치를 알려줌  
	PATH를 통해 찾아주기 때문에 PATH에 등록 안되어 있음 안알려줌

1. alias  
	alias [namespace]="[real cmd]"  
	현재 세션(shell)에서만 작동.  
	예를 들어 ll="ls -al"하면 ll하면 la -al해준다.  
	alias를 취소하는 방법은 unalias를 하면되고 취소하지 않고 명령어를 사용하려면(alias ls="ls f" 같은 경우) commed 또는 \후 명령어를 입력한다.  
1. shell variable
	쉘에도 변수를 설정할 수 있다.  
	[변수명]=[변수값] 하면 되는데 여기서 =와 변수값이나 명 사이에 공백이 있으면 안된다.  
	alias를 취소하는 방법은 unalias를 하면되고 취소하지 않고 명령어를 사용하려면(alias ls="ls f" 같은 경우) commed 또는 \후 명령어를 입력한다.  
1. shell variable
	쉘에도 변수를 설정할 수 있다.  
	[변수명]=[변수값] 하면 되는데 여기서 =와 변수값이나 명 사이에 공백이 있으면 안된다.  

# 2024. 05. 28
## linux
1. 파일  
	ls -l 하면 나오는 것들중 [---------- # name name # Day Time file]에서
	* name이 부분이 소유주와 소유그룹
	* ---------- 이 부분이 퍼미션 누구누구 권한 있는지를 알려주는 것 맨 앞은 파일인지 폴더인지 2번째부터 3개씩 나누어지며 각 소유자, 그룹, 그외 권한을 이야기 하고 또한 ---는 rwx를 가지고 있으며 r읽기 w쓰기 x실행을 의미한다. 예를 들면 -rwxrw-r-- 이면 소유자는 일고쓰고실행 가능하지만 그룹은 읽고 쓰기 그 외는 읽기만 가능해진다.
	* 폴더는 퍼미션 의미가 조금 달라진다. r는 ls같은 걸로 폴더내부 리스트를 읽어 올 수 있는가, w는 해당 폴더 안에 파일 및 폴더를 만들고 삭제 할 수 있는가, x는 폴더에 들어 갈 수 있는가를 의미한다.
	* 퍼미션은 chmod로 변경 가능하다(소유주와 root만 변경 가능)
1. su   
	su는 switch user의 약자로 유저를 변경하는 명령어다.   
	su 만 입력하면 root로 변경되는데 이때 환경변수등을 지금 그 상태로 가져간다. 그러므로 su -을 통해 환경변수를 가저가지 않게 해야 오류가 발생할 가능성이 적어진다. 
1. 표준 입력 출력 표준 에러  
	* 리다이렉션< > >> 2>
		* <는 읽기(텍스트파일은 파일 내용을 명령어면 명령어 실행결과를 넣어준다(< python !!.py 하면 파이선 결과값 넣어줌!!!)
		* `> 쓰기 왼쪽결과를 오른쪽에 파일로 써서 저장한다
		* `>>도 쓰기이지만 이어쓰기이다. >는 기존에 있던 파일을 덮어쓰기 해버려서 기존 결과가 사라지지만 >>는 뒤에 이어서 써준다.
		* 2>는 에러만 표준에러만 can't found같은거만 해준다.
		* /dev/null 여기다 리다이렉션 하면 아무것도 저장 안되고 쓰여지지도 않음 응용하면 에러만 화면에 출력 해줄 수 있게 하는 방식으로도 쓸 수 있다.
	* 파이프라인 |
		* 명령어와 명령어를 묶는 용도 find | grep에 많이 사용한다.
		* 왼쪽에서 오른쪽순서로 실행되고 먼저 실행된 값을 가지고 오른쪽에서 실행된다.
	* 필터 명령어 head, cat, tail less 등
		* head 앞쪽 부분을 볼 수 있음 디폴트값으로 10줄만 보여줌
		* 여러가지 있음

# 2024. 05. 29
## linux
1. text cmd  
	* wc  
		* -l line
		* -w word
		* -c char
	* sort
		* line cut sort
		* -n # chang sort
		* -r reverse
	* uniq
		* word uniq
		* but line defferent(line 1, line 2 X line 1, line 3 O) not remove
		* uniq is line count
	* cut
		* cut -d sep colnum filename
	* tr
		* tr is trans word
		* tr before after
		* tr is rex and only std input
	* tail
		* log catch many use... ????
		* tail -f filename <<<< This
1. grep
	* -i
		* grep is eq ascii but -i option is char eq(a == A)
	* rex
		* 'rex and word' use regex grep
		* Ex) ifconfig | grep inet <= only inet but ifconfig | grep "in?t" <= in[any char]t search
1. sed
	* stream cmd
	* similar vim :s
1. awk
	* pattern search
	* awk '/rex/ or pattern {action}' filename
	* Ex)
	> awk '$2 == 12 {print $1, $2}' score
	> awk '/ina*/ {print $1, $1} score
	* sed and awk is shell script many use
	* -F sep change

# 2024. 06. 14
## 뭐라 적어야 하지?
1. 일정
> 7/22 면접 준비(면접 실습)
> 이전에 자소서 완성필요
> 자소서에 스킬 넣기
> 전문지식, 경험
> 30초 스피치(작성 안해도 준비)
> 7/19 전에 자소서 작성
1. 자소서
> 기업 한개 정해서 작성
1. 필요능력
> 의사소통, 
> 문서작성

1. 면접에서
> * 면접관은 자소서 내용을 다 읽는건 아니다 핵심 문구를 읽는다. 그러니 자신의 강점을 모든곳에 녹여넣어라 물론 다르게 풀어서 적어야 한다.</br>
단 면접관이 너무 마음에 다라 갈 수 있기 때문에 운이 좀 따를 수 잇>?
1. 비전, 미션, 목표
> * 비>미>목 존재이유>그것을 위한 무언가>
|미션|내가 세상에 존재하는 목적은 무엇인가| |
|-|-|-|
||내가 세상에 기여하고 싶은 것은 무엇이며,세상에 기여할 수 있는 방법은 무엇인가.||
|비전|내가 장기적으로 이루고 싶은 목표는 무엇인가.(7년뒤 등)||
||7년뒤 내가어떤 모습이었으면 좋겠는가?||
|핵심가치|내가 가장 소중희 여기는 믿음과 신념은 무엇인가||
||내 모든 판단과 의사결정, 행동들은 어떤것을 목적을 가지고 하는가||
