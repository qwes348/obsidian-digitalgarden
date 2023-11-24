---
{"dg-publish":true,"permalink":"/Nfinity7/코이네코/코이네코 API/","tags":["gardenEntry"],"noteIcon":""}
---


---
[[Nfinity7/코이네코/코이네코 메모\|코이네코 메모]]

# 안쓰는건 취소선 처리 할 예정

## <span style='color:#8854d0'>초기 API들 (여전히 쓰는것도 있음)</span>

### 데이터셋 받아오기

```fold
/* desc:	공용 데이터셋 모두 획득
 * method:	post
 * url:		<http://54.180.106.167:52532/get_common>
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||type		|int		|데이터의 종류
 *		||array_data	|array int	|데이터 배열
 *		||desc		|string		|데이터 설명
 * desc:	공용으로 사용되는 데이터를 획득
 *		해당 데이터들은 국가별로 다를 필요가 없으며, 수치만 가짐
 */

 /* desc:	텍스트 데이터셋 모두 획득
 * method:	post
 * url:		<http://54.180.106.167:52532/get_text>
 *		|name		|type		|desc
 * input:	|country	|string		|국가 코드
 * output:	|code		|int		|0: 성공, 1: 실패
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||type		|int		|데이터의 종류
 *		||array_data	|array int	|데이터 배열
 *		||desc		|string		|데이터 설명
 * desc:	모든 텍스트 데이터를 획득
 *		현재 국가 코드는 ko(한글), en(영어)
 */
```

### 고양이 이름변경

```fold
/* desc:	캐릭터의 이름 변경
 * method:	post
 * url:		<http://54.180.106.167:52532/set_cat_name>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|uid_c		|string		|캐릭터의 고유값
 *		|name		|string		|변경하고자 하는 고양이 이름
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 고양이 없음, 3: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 * desc:	캐릭터의 이름을 원하는 문자열로 변경
 *		서버단에서 문자열 앞뒤의 무의미한 빈칸은 필터링하지만 확인은 필요함
 *		서버단에서 특수문자 및 이모지는 필터링하지만 확인은 필요함
 */
```

### 게시판 가져오기

```fold
/* desc:	게시판 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_boards>
 *		|name		|type		|desc
 * input:	|type		|int		|게시판의 종류
 *		|count		|int		|가져오는 게시물의 수
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 게시물 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||title		|string		|게시물의 제목
 *		||content	|string		|게시판의 본문
 *		||create_at	|string		|게시물이 작성된 일시
 * desc:	게시판에 저장된 게시물을 호출
 *		이때, 게시물은 가장 최근 생성된 것을 기준으로 내림차순 정렬됨
 *		제목 및 내용물에 길이 제한은 없음
 *		각 텍스트의 호출이 실제로 잘되는지 확인은 필요함
 */
```

### 바뀐 로그인

```fold
/* desc:	계정 정보를 이용해 로그인
 * method:	post
 * url:		<http://54.180.106.167:52531/user_login>
 *		|name		|type		|desc
 * input:	|email		|string		|메일 주소
 *		|nickname	|string		|닉네임, 필요 여부 확인 필요
 *		|type		|int		|0: 구글 로그인, 1: 이메일 로그인
 *		|password	|string		|비밀번호, 구글 로그인일 시 없어도 됨
 * output:	|code		|int		|0: 가입 및 로그인 성공, 1: 이메일 조회 실패, 2: 비밀번호 틀림, 3: 아이디 생성 실패, 4: 계정 생성 결과 조>회 실패, 5: 구글 로그인시 계정 생성 및 로그인 성공
 *		|data		|json		|
 *		||uid		|string		|계정 고유값
 *		||email		|string		|계정 이메일
 *		||nickname	|string		|닉네임
 *		||gold		|int		|소지 골드
 *		||cash		|int		|소지 캐시
 *		||home_max	|int		|캐터리 최대 보관수
 *		||egg_max	|int		|알 보유 가능 최대 개수
 *		||type		|int		|0: 구글 로그인, 1: 이메일 로그인
 *		||level		|int		|계정의 레벨
 *		||exp		|int		|계정의 경험치
 *		||point		|int		|계정의 잔여 스킬 포인트
 *		||skill		|array int	|계정의 스킬 레벨 배열
 *		||correction	|array in	|계정의 스킬 레벨 보정치 배열
 *		|message	|string		|반환 메세지
 */
```

### 바뀐 고양이 목록

```fold
/* desc:	유저의 고양이 목록을 받아옴
 * method:	post
 * url:		<http://54.180.106.167:52532/get_cats>
 *		|name		|type		|desc
 * input:	|uid		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 성공 - 고양이 없음
 *		|message 	|string		|실패 사유
 *		|data	 	|json		|
 *		||count		|int		|고양이 마릿수
 *		||list		|array string	|
 *		|||uid		|string		|고양이의 uid
 *		|||uid_u	|string		|현재 주인의 uid
 *		|||uid_o	|string		|최초 주인의 uid
 *		|||uid_c_dad	|string		|아빠 고양이의 uid, seed 고양이일때 null
 *		|||uid_c_mom	|string		|엄마 고양이의 uid, seed 고양이일때 null
 *		|||date_cur	|int		|고양이의 잔여 교배 횟수
 *		|||date_max	|int		|고양이의 최대 교배 횟수
 *		|||name		|string		|고양이의 이름
 *		|||stat		|json		|캐터리에서의 능력치
 *		|||status	|int		|0: 알, 1: 유년, 2: 성년, 3: NFT
 *		|||is_in_home	|int		|고양이가 캐터리 안에 들어가 있는가?
 *		|||is_seed	|int		|0: seed 아님, 1: seed 맞음
 *		|||evolve_left	|int		|진화까지 필요한 시간(초)
 *		|||evolve_at	|datetime	|진화하는 일시
 *		|||can_evolve	|int		|0: 진화 불가, 1: 진화 가능
 * desc:	현재 계정에서 키우고 있는 고양이를 반환
 *		단, NFT화된 고양이는 반환하지 않음
 */
```

### 바뀐 고양이 상세정보

```fold
/* desc:	고양이의 상세 정보를 획득
 * method:	post
 * url:		<http://54.180.106.167:52532/get_cat>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|고양이 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message 	|string		|실패 사유
 *		|data	 	|int		|고양이 보유 수
 *		||stat		|array json	|
 *		|||gen_dec	|array int	|유전자값, 배열 번호로! 능력치: 0 - 5, 외형: 6 - 24
 *		|||gen_max	|array int	|각 유전자가 가질 수 있는 최대값
 *		||uid_o	 	|string		|최초로 생성한 이용자 고유값
 *		||uid_c_dad	|string		|아빠 고양이의 고유값
 *		||uid_c_mom	|string		|엄마 고양이의 고유값
 *		||name		|string		|고양이의 이름
 *		||name_dad	|string		|아빠 고양이의 이름
 *		||name_mom	|string		|엄마 고양이의 이름
 *		||cond		|array int	|
 *		||is_in_home	|int		|고양이가 캐터리 안에 들어가 있는가?
 *		||evolve_left	|int		|진화까지 필요한 시간(초)
 *		||evolve_at	|datetime	|진화하는 일시
 *		||can_evolve	|int		|0: 진화 불가, 1: 진화 가능
 * desc:	고양이에 대한 상세 정보를 획득
 *		능력치라던지 캐터리에서의 상태값이라던지 그냥 싹 가져옴
 */
```

### 다마고치 정보 가져오기

```fold
/* desc:	다마고치 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_home>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 캐릭터 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||uid		|string		|캐릭터의 고유값
 *		||name		|string		|이름
 *		||stat		|array int	|다마고치 능력치
 *		||status	|string		|0: 알(볼 일 없음), 1: 유년, 2: 성년, 3: NFT(볼 일 없음)
 * desc:	캐터리 안에 존재하는 캐릭터만 리스트로 호출
 */
```

### 계정 경험치 테이블 가져오기

```fold
/* desc:	계정 경험치 테이블 가져오기
 * method:	post
 * url:		<http://13.124.70.239:52532/get_exp_table>
 *		|name		|type		|desc
 * input:	|level		|int		|현재 레벨 값, 없어도 됨
 * output:	|code		|int		|0: 성공
 *		|message	|string		|
 *		|data		|array int	|각 레벨당 필요 경험치
 * desc:	각 레벨마다 필요한 경험치 수치를 호출
 *		만약 level 값을 입력했다면, 현재 레벨에 해당하는 경험치 배열을(길이 1) 반환
 *		만약 level 값이 없다면, 255레벨까지의 필요 경험치 배열을 반환
 */
```

### 스킬 포인트를 사용하여 스킬의 레벨을 올리고 관련 정보를 가져오기

```fold
/* desc:	스킬 포인트를 사용하여 스킬의 레벨을 올리고 관련 정보를 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_skill>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|skill_slot	|int		|배열에서의 스킬 번호, 0번부터 5번까지
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - 스킬 포인트 없음, 4: 실패 - 스킬 레벨 50 초과, 5: 실패 - update_00, 6: 실패 - select_01
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||level		|int		|현재 레벨
 *		||exp		|int		|현재 경험치
 *		||point		|int		|잔여 스킬 포인트
 *		||skill		|array int	|현재 스킬 레벨 배열
 * desc:	이용자의 고유값 및 레벨을 올리고자 하는 스킬의 배열 번호로 작동
 *		만약 스킬 포인트가 없는 상태라면 실패를 반환
 *		스킬 포인트가 남는다 하더라도 레벨 50을 넘어가면 실패를 반환
 */
```

### 획득한 경험치를 계정 정보에 반영하고, 반영된 값을 가져오기

```fold
/* desc:	획득한 경험치를 계정 정보에 반영하고, 반영된 값을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_exp>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|exp		|int		|획득한 경험치
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - update_00, 4: 실패 - select_01
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||level		|int		|현재 레벨
 *		||exp		|int		|현재 경험치
 *		||point		|int		|잔여 스킬 포인트
 * desc:	획득한 경험치를 통해 계정 정보를 변경하고 변경된 값들을 반환
 *		경험치에 따라 레벨을 계정의 레벨을 증가시킴
 *		레벨 증가로 인해 스킬 포인트를 획득한다면 해당 사항 반영하여 반환
 *		레벨업에 사용된 경험치를 제외한 나머지 수치 역시 잔여 경험치로써 반영됨
 *		레벨업이 안됐다면 그냥 계정의 경험치만 증가시킴
 */
```

### 획득한 경험치를 계정 정보에 반영하고, 반영된 값을 가져오기\_Ver2

```fold
/* desc:	획득한 경험치를 계정 정보에 반영하고, 반영된 값을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_exp_ver2>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|exp		|int		|획득한 경험치
 *		|dist		|int		|달리기 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - update_00, 4: 실패 - update_01, 5: 실패 - 경험치 비교 실패
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||level		|int		|현재 레벨
 *		||exp		|int		|현재 경험치
 *		||point		|int		|잔여 스킬 포인트
 * desc:	획득한 경험치를 통해 계정 정보를 변경하고 변경된 값들을 반환
 *		경험치에 따라 레벨을 계정의 레벨을 증가시킴
 *		레벨 증가로 인해 스킬 포인트를 획득한다면 해당 사항 반영하여 반환
 *		레벨업에 사용된 경험치를 제외한 나머지 수치 역시 잔여 경험치로써 반영됨
 *		레벨업이 안됐다면 그냥 계정의 경험치만 증가시킴
 *		경험치는 달린 거리 152당 1씩 증가하며 버림 연산 (ex. 1000 / 152 = 6.5789 := 6)
 */
```

### 달리기 게임에 사용되는 스킬의 레벨 및 증감치를 가져오기 ⇒ 최종 스킬 증감치 가져오기

```fold
/* desc:	달리기 게임에 사용되는 스킬의 레벨 및 증감치를 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_run_skill>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - select_01, 4: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||arr_merge	|array int	|계정 및 캐릭터의 스킬 레벨 합산 배열
 *		||arr_value	|array int	|최종 스킬 증감치 배열
 * desc:	계정과 캐릭터로부터 각각 스킬 레벨을 합산하고 반환
 *		알 상태이거나 NFT 상태라면 실패(2)를 반환
 *		만약 캐릭터가 아직 유년기 상태라면 스킬 레벨은 절반(버림 연산)만 가산됨
 *		arr_skill_v는 합산된 스킬 레벨에 따른 증감치를 담음
 *		이때, 각 증감치는 게임에 적용되어 있는 기본값을 기준으로 퍼센트 감가산이 기본
 *		ex) 기본값 10, 증감치 76 -> 10 + (10 * 0.76) = 17.6, 필요에 따라 버림 연산 적용
 */
```

### 캐릭터의 캐터리 보관 여부를 토글하기

```fold
/* desc:	캐릭터의 캐터리 보관 여부를 토글하기
 * method:	post
 * url:		<http://54.180.106.167:52532/toggle_home>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - update_00, 4: 실패 - select_01, 5: 실패 - 그런 이용자 없음, 6: 실패 - select_02, 7: 실패 - 캐터리 정원 초과, 8: 실패 - update_01
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||uid_c		|string		|캐릭터의 고유값
 *		||is_in_home	|int		|0: 이제 캐터리에서 빠진 상태임, 1: 이제 캐터리에 추가된 상태임
 * desc:	캐릭터와 캐터리의 관계를 토글함
 *		만약 현재 캐터리에 들어가 있는 캐릭터라면 제거됨
 *		만약 현재 캐터리에 있지 않은 캐릭터라면 추가됨
 *		단, 캐터리 최대 보관수를 초과할 수는 없음
 */
```

### 다마고치 액션 및 그에 따른 변경점 가져오기

```fold
/* desc:	다마고치 액션 및 그에 따른 변경점 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_home_action>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 *		|num_action	|int		|액션의 배열 번호(0~5)
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 공용 정보 없음, 3: 실패 - select_01, 4: 실패 - 캐릭터 없음, 5: 실패 - select_02, 6: 실패 - 그런 이용자 없음, 7: 실패 - 골드 부족, 8: 실패 - update_00, 9: 실패 - update_01, 10: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||uid_u		|string		|이용자의 고유값
 *		||uid_c		|string		|캐릭터의 고유값
 *		||now_gold	|int		|이제 남은 골드
 *		||spend_gold	|int		|액션을 수행하는데 소모한 골드
 *		||arr_stat	|array int	|액션을 수행하고 난 이후의 고양이 능력치(행복 등)
 *    ||evolve_left | int  |진화 남은시간
 * desc:	다마고치에서 액션을 수행하고, 그 결과를 반환
 *		각 액션마다 소모되는 재화 이상의 재화를 보유하고 있어야만 함
 *		지출한 골드 및 계정에 남은 골드를 반환하며, 캐릭터의 마다고치상 능력치 배열을 반환
 *		능력치 배열상 결과값이 0보다 작아지면 0을, 100보다 커지면 100을 반환
 */
```

### 캐릭터의 진화 시도하고 변경된 정보 가져오기

```fold
/* desc:	캐릭터의 진화 시도하고 변경된 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_evolve>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - 유년기가 아님, 4: 실패 - 진화 조건을 충족하지 않았음, 5: 실패 - 그런 공용 정보 없음, 6: 실패 - update_00, 7: 실패 - select_02, 8: 실패 - 그런 캐릭터 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||uid		|string		|캐릭터의 고유값
 *		||name		|string		|캐릭터의 이름
 *		||stat		|array int	|진화 시도 이후 변경된 능력치값
 *		||status	|int		|현재 상태, 0: 알, 1: 유년기, 2: 성년기, 3: NFT
 *		||is_in_home	|int		|캐터리에 보관된 캐릭터인지 여부
 *		||is_seed	|int		|시드 캐릭터 여부
 * desc:	캐릭터의 능력치(행복 등) 중 하나라도 100에 도달했다면 진화를 시도
 *		복수개의 항목이 동시에 100에 도달했다면 모든 확률을 합하여 진행
 *		진화는 성공하건 실패하건 100에 도달했던 모든 능력치는 절반으로 감소됨
 */
```

### 시즌 스테이지를 시작하고 스테이지 정보 가져오기

```fold
/* desc:	시즌 스테이지를 시작하고 스테이지 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_season_begin>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 시즌 시드값 없음, 3: 실패 - select_01, 4: 실패 - 그런 캐릭터 없음, 5: 실패 - insert_00, 6: 실패 - 세션 이미 존재, 7: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||stage		|array string	|스테이지를 구성하는 숫자(문자열)의 배열
 *		||seed		|int		|스테이지를 생성하는데 사용된 seed 값
 *		||uid_s		|int		|시즌의 고유값
 *		||uid_g		|int		|게임의 고유값
 *		||uid_u		|int		|이용자의 고유값
 *		||uid_c		|int		|캐릭터의 고유값
 *		||max_dist	|int		|내가 달성한 최고 기록, 만약 없다면 0을 반환
 * desc:	고양이의 정보를 받아 새로운 게임을 생성
 *		시즌 게임에 대한 시작만을 담당
 *		현재 시즌에 따라 총 1024 개의 스테이지 배열을 반환
 *		3월 이후부터 시드값이 바뀔 예정이므로 스테이지 구성이 변경될 것
 */
```

### 비시즌 스테이지를 시작하고 스테이지 정보 가져오기

```fold
/* desc:	비시즌 스테이지를 시작하고 스테이지 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_normal_begin>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_01, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - insert_00, 4: 실패 - 세션 없음, 5: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||stage		|array string	|스테이지를 구성하는 숫자(문자열)의 배열
 *		||seed		|int		|스테이지를 생성하는데 사용된 seed 값
 *		||uid_s		|int		|비시즌이기 때문에 그냥 null
 *		||uid_g		|int		|게임의 고유값
 *		||uid_u		|int		|이용자의 고유값
 *		||uid_c		|int		|캐릭터의 고유값
 *		||max_dist	|int		|내가 달성한 최고 기록, 만약 없다면 0을 반환
 * desc:	고양이의 정보를 받아 새로운 비시즌 게임을 생성
 *		비시즌 게임에 대한 시작만을 담당
 *		랜덤한 시드 값을 통해 생성된 총 1024 개의 스테이지 배열을 반환
 */
```

### ~~러닝 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기~~ 대체됨 2023-10-18

```fold
/* desc:	러닝 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기
 * method:	post
 * url:		<http://$>{host}:52534/set_game_end
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||get_exp	|int		|경험치
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|10위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||now		|json		|이번 게임 기록
 *		|||is_season	|int		|0: 비시즌, 1: 시즌
 *		|||dist		|int		|도달 거리
 *		|||gold		|int		|획득 골드
 *		|||cash		|int		|획득 캐시
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||name		|string		|캐릭터의 닉네임
 * desc:	게임을 종료하고 필요한 값을 반환
 *		rank 는 내가 달성했던 기록중 가장 랭킹이 높은 게임 기록
 *		ranking 은 서버상 존재하는 가장 랭킹이 높은 10개의 게임 기록 배열
 *		now 는 이번 게임에서 달성한 기록
 */
```

### 스테이지를 진행하고 있는 중간중간 진행 정보 저장하기

```fold
/* desc:	스테이지를 진행하고 있는 중간중간 진행 정보 저장하기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_game_mid>
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 * desc:	스테이지 진행 중간마다 플레이 기록을 저장하고 게임의 정상 진행 여부를 반환
 *		현재 거리 1000, 골드 1000, 캐시 100 이상 차이날 때, 및 각각 차이가 0일 때 오류(3) 반환
 */
```

### 현재 사용하지 않는 부화장치들을 가져오기

```fold
/* desc:	현재 사용하지 않는 부화장치들을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_incu_empty>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 남는 부화기 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||count_same	|int		|부화기의 수량
 *		||count		|int		|잔여 부화 가능 횟수
 *		||type		|int		|0: 무한 부화기, 1: 유료 부화기
 * desc:	현재 사용중이 아닌 부화기들의 정보를 호출
 *		포켓몬고와 너무 유사하기 때문에 차별성에 대한 고민이 필요할지도 모름...
 */
```

### 알 목록을 가져오기

```fold
/* desc:	알 목록을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_eggs>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 0: 성공 - 가진 알이 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||is_in_incu	|int		|0: 부화기 사용 중, 1: 방치되는 중
 *		||uid		|string		|캐릭터의 고유값
 *    ||name		|string		|캐릭터의 이름
 *		||end_at	|string		|부화가 되는 시간
 *		||sec_left	|int		|부화에 필요한 남은 시간(초)
 *		||ti_type		|int		|0: 무료 부화기, 1: 유료 부화기, 2: 부화기 사용중이 아님
 * desc:	현재 보유하고 있는 모든 알을 호출
 *		이때, 부화기에 들어가 있는 알이 먼저 나오고 그렇지 않은 알이 뒤에 나오게 됨
 *		알이 부화하는 정확한 시간은 end_at이지만 현재 시간과의 계산이 어려운 경우를 위해 sec_left를 함께 전송
 *		sec_left는 알 목록에서 부화시간을 표시하는 용도로 쓰면 괜찮지만 보기에 어색할시 퇴출될 수 있음
 */
```

### 알로부터 캐릭터를 부화시키고, 해당 캐릭터의 상세 정보를 가져오기

```fold
/* desc:	알로부터 캐릭터를 부화시키고, 해당 캐릭터의 상세 정보를 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_egg_hatch>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|고양이 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 알 없음, 3: 실패 - 아직 부화시간 안됨, 4: 실패 - update_00, 5: 실패 - update_01, 6: 실패 - select_00
 *		|message 	|string		|실패 사유
 *		|data	 	|int		|고양이 보유 수
 *		||stat		|array json	|
 *		|||gen_dec	|array int	|유전자값, 배열 번호로! 능력치: 0 - 5, 외형: 6 - 24
 *		|||gen_max	|array int	|각 유전자가 가질 수 있는 최대값
 *		|uid_o	 	|string		|최초로 생성한 이용자 고유값
 *		|uid_c_dad	|string		|아빠 고양이의 고유값
 *		|uid_c_mom	|string		|엄마 고양이의 고유값
 *		|name		|string		|고양이의 이름
 *		|name_dad	|string		|아빠 고양이의 이름
 *		|name_mom	|string		|엄마 고양이의 이름
 *		|cond		|array int	|
 *		|is_in_home	|int		|고양이가 캐터리 안에 들어가 있는가?
 * desc:	고양이에 대한 상세 정보를 획득
 *		능력치라던지 캐터리에서의 상태값이라던지 그냥 싹 가져옴
 */
```

### 스킬 레벨에 따른 증감치 테이블 가져오기

```fold
/* desc:        스킬 레벨에 따른 증감치 테이블 가져오기
 * method:      post
 * url:         <http://54.180.106.167:52532/get_skill_table>
 *              |name           |type           |desc
 * input:       |level          |int            |현재 레벨 값, 없어도 됨
 * output:      |code           |int            |0: 성공
 *              |message        |string         |
 *              |data           |array int      |각 레벨당 증감치
 * desc:        각 스킬이 레벨에 따라 가지는 증감 수치를 호출
 *              만약 level 값을 입력했다면, 현재 레벨에 해당하는 스킬 증감치를(길이 1) 반환
 *              만약 level 값이 없다면, 50레벨까지의 스킬 증감치 배열을 반환
 */
```

### 리더보드 정보를 획득 (로비에서)

```fold
/* desc:	리더 보드 정보를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_game_ranks
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|is_season	|int		|0: 비시즌, 1: 시즌
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 시즌 없음, 3: 실패 - select_01, 4: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|50위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|string		|1: 유아체, 2: 성체
 * desc:	내 이용자 고유값과 시즌 여부를 통해 해당하는 리더 보드를 호출
 *		리더보드는 나의 최고 기록을 포함하지만 정보가 없다면 각각 빈 배열로 반환될 것
 */
```

### 알을 부화기 안에 넣고 해당하는 결과값을 가져오기

```fold
/* desc:	알을 부화기 안에 넣고 해당하는 결과값을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_incu_egg>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|uid_c		|string		|캐릭터의 고유값
 *		|type		|int		|0: 무료 부화기, 1: 유료 부화기
 *		|count		|int		|선택된 부화기의 남은 횟수
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 부화기 없음, 3: 실패 - update_00, 4: 실패 - select_01
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||uid_i		|string		|부화기의 고유값, 큰 의미 없음
 *		||uid_c		|string		|캐릭터의 고유값
 *		||uid_u		|string		|이용자의 고유값, 큰 의미 없음
 *		||type		|int		|0: 무료 부화기, 1: 유료 부화기
 *		||count		|int		|-1: 무료 부화기, 0 > 유료 부화기의 남은 사용 횟수
 *		||sec_left	|int		|부화에 필요한 남은 시간(초)
 * desc:	사실상 성공했는지 실패했는지만 알아도 동작 자체는 무방한 기능
 *		부화기를 선택하는방법에 따라 구현되는 모습이 조금 달라질 수 있음
 *		1: 부화기를 남은 횟수 종류별로 선택, 2: 무료 부화기, 유료 부화기 둘 중 하나를 선택 등등
 *		남은 시간은 함수로부터 리턴받는 시점부터 적용됨
 */
```

### 데이트시작을 알리고 UID 받아오기

```fold
/* desc:	데이트 시작을 알리고 UID 받아오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_date>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|uid_c_dad	|string		|아빠 캐릭터의 고유값
 *		|uid_c_mom	|string		|엄마 캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 그런 이용자 없음, 3: 실패 - select_01, 4: 실패 - 아빠 없음, 5: 실패 - 아빠 데이트 못함, 6: 실패 - select_02, 7: 실패 - 엄마 없음, 8: 실패 - 엄마 데이트 못함, 9: 실패 - 동성 결혼, 10: 실패 - select_03, 11: 실패 - 알 슬롯 부족, 12: 실패 - insert_00, 13: 실패 - select_03
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_d		|string		|데이트의 고유값
 *		||uid_u		|string		|이용자의 고유값
 *		||uid_c_dad	|string		|아빠 캐릭터의 고유값
 *		||uid_c_mom	|string		|엄마 캐릭터의 고유값
 * desc:	데이트를 했다는 기록 자체를 남기는데 의미가 있음
 *		이후 해당 기록을 기반으로 새로운 알을 획득
 */
```

### 데이트 끝을 알리고 알을 받아오기

```fold
/* desc:	데이트 끝을 알리고 알을 받아오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_egg>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|uid_d		|string		|데이트의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 그런 데이트 없음, 3: 실패 - update_00, 4: 실패 - insert_00, 5: 실패 - update_01, 6: 실패 - select_01, 7: 실패 - 새끼 안 만들어짐
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_c		|string		|알의 고유값
 *		||uid_u		|string		|이용자의 고유값
 *		||uid_c_dad	|string		|아빠 캐릭터의 고유값
 *		||uid_c_mom	|string		|엄마 캐릭터의 고유값
 *		||status	|string		|0: 알(보통 당연히 알만 갈 것), 1: 유년, 2: 성년, 3: NFT
 *		||stat		|string		|다마고치 내에서의 상태(보통 당연히 [0,0,0,0,0]만 갈 것)
 * desc:	올바르게 데이트를 수행한 적이 있다면 해당 데이트를 종료하고 알을 획득
 *		해당 알은 부모의 유전자 값을 유전자로 물려 받은 상태임
 *		교배 가능 횟수는 본 함수를 호출하여 자식을 획득했을 때 각각 1씩 차감됨
 */
```

### 상점에서 판매중인 캐시의 목록을 가져오기

```fold
/* desc:	상점에서 판매중인 캐시의 목록을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_shop_cash>
 *		|name		|type		|desc
 * input:	|country	|string		|이용자의 국가코드
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 상점 아이템 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||uid_sc	|string		|상점 아이템의 고유값
 *		||name		|string		|아이템의 이름
 *		||price		|int		|아이템의 가격
 *		||amount	|int		|획득할 수 있는 캐시의 양
 * desc:	이용자가 구매할 수 있는 캐시 목록을 획득
 */
```

### 상점에서 캐시를 구입하고 결과값 가져오기

```fold
/* desc:	상점에서 캐시를 구입하고 결과값 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_shop_cash>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|uid_sc		|string		|상점 아이템의 고유값
 *		|country	|string		|이용자의 국가코드
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 그런 이용자 없음, 3: 실패 - select_01, 4: 실패 - 그런 상품 없음, 5: 실패 - update_00, 6: 실패 - select_00, 7: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u		|string		|이용자의 고유값
 *		||cash		|int		|구매된 이후 이용자가 가지는 캐시 잔고
 * desc:	캐시를 구매하고 구매 내역을 계정에 반영
 */
```

### 캐시를 골드로 변환하고 결과값을 가져오기

```fold
/* desc:	캐시를 골드로 변환하고 결과값을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_cash_to_gold>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|cash		|int		|골드 교환에 사용할 캐시의 양
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 그런 이용자 없음, 3: 실패 - 캐시 없음, 4: 실패 - select_01, 5: 실패 - 교환 데이터 없음, 6: 실패 - update_00, 7: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u		|string		|이용자의 고유값
 *		||gold		|int		|캐시 교환 이후 골드 잔고
 *		||cash		|int		|캐시 교환 이후 캐시 잔고
 * desc:	캐시를 교환하고 해당하는 내역을 골드에 반영
 *		골드 교환 비율에 대한 데이터는 get_common의 type=7, 현재는 30
 */
```

### 알 슬롯 최대 개수를 증가시키고 상응하는 골드를 차감

```fold
/* desc:	알 슬롯 최대 개수를 증가시키고 상응하는 골드를 차감
 * method:	post
 * url:		<http://54.180.106.167:52532/set_egg_max>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 공용 데이터 없음, 3: 실패 - select_01, 4: 실패 - 그런 이용자 없음, 5: 실패 - 돈 없음, 6: 실패 - update_00, 7: 실패 - select_01, 8: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u		|string		|이용자의 고유값
 *		||gold		|int		|슬롯 확장 이후 골드 잔고
 *		||egg_max	|int		|슬로 확장 이후 알 최대 슬롯
 * desc:	알 슬롯 최대치를 상승시킴
 *		참고로 알 슬롯 확장에 드는 비용 및 확장되는 개수는 common 테이블의 type 11 에 ["6000","3"]처럼 저장되어 있음
 */
```

### 캐터리 슬롯 최대 개수를 증가시키고 상응하는 골드드를 차감

```fold
/* desc:	캐터리 슬롯 최대 개수를 증가시키고 상응하는 골드를 차감
 * method:	post
 * url:		<http://54.180.106.167:52532/set_home_max>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 공용 데이터 없음, 3: 실패 - select_01, 4: 실패 - 그런 이용자 없음, 5: 실패 - 돈 없음, 6: 실패 - 캐터리 확장이 이미 최대, 7: 실패 - update_00, 8: 실패 - select_01, 9: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u		|string		|이용자의 고유값
 *		||gold		|int		|슬롯 확장 이후 골드 잔고
 *		||home_max	|int		|슬로 확장 이후 캐터리 최대 슬롯
 * desc:	캐터리 슬롯 최대치를 상승시킴
 *		참고로 캐터리 슬롯 확장에 드는 비용 및 확장되는 개수는 common 테이블의 type 12 에 ["6000","12000","24000","48000","5"]처럼 저장되어 있음
 *		[0~3] 는 각 단계별 슬롯 확장에 필요한 코인의 개수
 *		[4] 는 캐터리를 확장할 수 있는 최대 단계, 현재 1가 기본값이므로 확장 가능한 수는 1 + 4 = 5 개임
 */
```

### 캐릭터의 진화 시도하고 변경된 정보 가져오기

```fold
/* desc:	캐릭터의 진화 시도하고 변경된 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/set_evolve>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - 유년기가 아님, 4: 실패 - 진화 조건을 충족하지 않았음, 5: 실패 - update_00, 6: 실패 - select_02, 7: 실패 - 그런 캐릭터 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||uid		|string		|캐릭터의 고유값
 *		||name		|string		|캐릭터의 이름
 *		||stat		|array int	|진화 시도 이후 변경된 능력치값
 *		||status	|int		|현재 상태, 0: 알, 1: 유년기, 2: 성년기, 3: NFT
 *		||is_in_home	|int		|캐터리에 보관된 캐릭터인지 여부
 *		||is_seed	|int		|시드 캐릭터 여부
 * desc:	진화활 때가 된 캐릭터에 대한 진화를 수행
 */
```

### 고양이와 이별

```fold
/* desc:	캐릭터와의 이별
 * method:	post
 * url:		<http://54.180.106.167:52532/set_cat_farewell>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없거나 seed 캐릭터임, 3: 실패 - update_00
 *		|message	|string		|반환 메세지
 *		|data		|string		|캐릭터의 고유값
 */
```

### 새로운 부화기를 구매하고, 현재 빈 부화기의 개수 및 남은 골드를 가져오기

```fold
/* desc:	새로운 부화기를 구매하고, 현재 빈 부화기의 개수 및 남은 골드를 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52532/get_incu_new>
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - update_00, 4: 실패 - insert_00, 5: 실패 - select_01, 6: 실패 - 부화기 없음, 7: 실패 - select_02, 8: 실패 - 공용 데이터 없음, 9: 실패 - 돈 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||arr_incu	|array json	|
 *		|||count_same	|int		|부화기의 수량
 *		|||count	|int		|잔여 부화 가능 횟수
 *		|||type		|int		|0: 무한 부화기, 1: 유료 부화기
 *		||gold		|int		|남은 골드
 * desc:	현재 사용중이 아닌 부화기들의 정보를 호출
 *		계정에 남은 골드도 같이 호출
 */
```

### 런게임에서 탈주

```fold
/* desc:	게임에서의 탈주(시즌, 비시즌 공용)
 * method:	post
 * url:		<http://54.180.106.167:52532/set_game_escape>
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|-		|-
 * desc:	달리기 게임 도중 일시정지를 누르고 탈주할 때 등에 사용
 *		정상 탈주 여부는 code를 통해 확인하며 0일 때만 동작한다고 보면 됨
 *		하지만 어차피 탈주가 목적인데다 세션이 2분 지속되므로 실패해도 에러 메세지를 띄우고 탈주하면 될 듯
 */
```

---

### 이용자가 보유한 모든 친구 목록을 획득

```fold
/* desc:	이용자가 보유한 모든 친구 목록을 획득
 * method:	post
 * url:		<http://$>{host}:52536/get_frnds
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - get_not, 4: 실패 - get_add, 5: 실패 - get_added
 *		|message	|string		|실패 사유
 *		|data		|json array	|
 *		||uid_u		|string		|친구의 고유값
 *		||nickname	|string		|친구의 닉네임
 *		||level		|string		|친구의 레벨
 *		||is_accept	|int		|친구 수락 여부
 *		||uid_f		|string		|친구 테이블 상에서의 고유값
 *		||is_my_apply	|int		|0: 친구 신청 당함, 1: 친구 신청함
 *		||ranking	|int		|이번 시즌 친구의 순위
 *		||max_dist	|int		|이번 시즌 최대 도달 거리
 *		||uid_c		|string		|이번 시즌 등록 캐릭터 고유값
 *		||status	|int		|1: 유아체, 2: 성년체
 *		||icon_tx	|int		|0: 안보냄, 1: 보냄, 2: 받음(1과 2는 동일하게)
 *		||icon_rx	|int		|0: 안받음, 1: 수령 가능, 2: 수령 완료
 * desc:	현재 나와 관계된 모든 친구 목록을 불러옴
 *		반환되는 배열의 순서는 다음과 동일
 *		신청 상태 -> 내가 먼저 신청한 친구 -> 내가 신청 당한 친구
 *
 */
```

### 친구(친구 신청 상태 포함)를 삭제

```fold
/* desc:	친구(친구 신청 상태 포함)를 삭제
 * method:	post
 * url:		<http://$>{host}:52536/set_delete
 *		|name		|type		|desc
 * input:	|uid_f		|string		|친구 테이블 상에서의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - delete_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_f		|string		|삭제된 친구 테이블 상에서의 고유값
 * desc:	친구로 엮여 있는 모든 관계를 삭제
 *		단, 이미 주고 받은 선물은 최대 12시간 동안 유효
 *		다시 친구 등록을 하고 선물을 주고 받을때 동일하게 지속됨
 */
```

### 선물을 받는 기능

```fold
/* desc:	선물을 받는 기능
 * method:	post
 * url:		<http://$>{host}:52536/set_present_rx
 *		|name		|type		|desc
 * input:	|uid_u_tx	|string		|선물을 보내는 이용자의 고유값
 *		|uid_u_rx	|string		|선물을 받는 이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - set_present_tx, 2: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u_tx	|string		|선물을 보내는 이용자의 고유값
 *		||uid_u_rx	|string		|선물을 받는 이용자의 고유값
 *		||cash	|string		|선물을 통해 획득한 젤리의 양
 * desc:	선물을 받는 기능
 *		그냥 code만 0이면 성공
 */
```

### 선물을 보내는 기능

```fold
/* desc:	선물을 보내는 기능
 * method:	post
 * url:		<http://$>{host}:52536/set_present_tx
 *		|name		|type		|desc
 * input:	|uid_u_tx	|string		|선물을 보내는 이용자의 고유값
 *		|uid_u_rx	|string		|선물을 받는 이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - set_present_tx, 2: 실패 - 발신수신 동일
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u_tx	|string		|선물을 보내는 이용자의 고유값
 *		||uid_u_rx	|string		|선물을 받는 이용자의 고유값
 * desc:	선물을 전송하는 기능
 *		그냥 code만 0이면 성공
 */
```

### 존재하는 친구 신청을 수락하기

```fold
/* desc:	존재하는 친구 신청을 수락하기
 * method:	post
 * url:		<http://$>{host}:52536/set_frnd_accept
 *		|name		|type		|desc
 * input:	|uid_f		|string		|친구 테이블 상에서의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 친구 신청 없음, 3: 실패 - update_00, 4: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_f		|string		|친구 테이블상에서의 고유값
 * desc:	친구 테이블상에서의 고유값을 이용해 해당 신청을 수락 상태로 변경
 */
```

### 친구 코드에 대응되는 이용자에게 친구 신청하기

```fold
/* desc:	친구 코드에 대응되는 이용자에게 친구 신청하기
 * method:	post
 * url:		<http://$>{host}:52536/set_frnd
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|code_f		|string		|친구 신청용 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - select_00, 4: 실패 - 이미 친구임, 5: 실패 - insert_00, 6: 실패 - insert_00, 7: 실패 - 발신수신 동일
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u_00	|string		|이용자의 고유값
 *		||uid_u_01	|string		|친구의 고유값
 * desc:	친구 신청을 위한 고유값을 이용하여 대응되는 친구에게 친구 상태가 되는 것을 신청
 */
```

### 이용자 고유값을 입력하고 친구 코드를 가져오기

```fold
/* desc:	이용자 고유값을 입력하고 친구 코드를 가져오기
 * method:	post
 * url:		<http://$>{host}:52536/get_frnd_code
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - 그런 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||code_f	|string		|친구 코드
 * desc:	이용자의 고유값을 입력하면 대응되는 고유 친구 코드값을 반환
 */
```

### 메뉴 뱃지 받아오기

```fold
/* desc:	각 아이콘의 배지를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_badge
 *		|name		|type		|desc
 * input:	|uid_u	        |string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 이용자 없음, 3: 실패 - select_01, 4: 실패 - 이벤트 없음, 5: 실패 - select_02, 6: 실패 - 공지 없음,
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||frnd_has_new	|int		|0: 받은 신청 없음, 1: 받은 신청 있음
 *		||frnd_cnt	|int		|받은 신청의 개수
 *		||event_has_new	|int		|0: 새 이벤트 없음, 1: 새 이벤트 있음
 *		||event_cnt	|int		|새 이벤트의 개수
 *		|||int		|0: 새 공지 없음, 1: 새 공지 있음
 *		||notice_cnt	|int		|새 공지의 개수
 * desc:	친구, 공지, 이벤트 중 새로 생긴 것을 반환함
 *		친구는 수락을 하거나 거절을 하지 않는 이상 계속 노출
 *		공지 및 이벤트는 현재 시점에서 2일 동안 새 것이 있으면 노출
 */
```

### 현재 버전 받아오기

```fold
/* desc:	버전 정보 확인
 * method:	post
 * url:		<http://$>{host}:52531/get_version
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|data		|string		|버전 정보(ex: 1.0.0)
 */
```

### 닉변

```fold
/* desc:        계정의 닉네임을 변경
 * method:      post
 * url:         <http://$>{host}:52532/set_nickname
 *              |name           |type           |desc
 * input:       |uid_u          |string         |이용자의 고유값
 *              |nickname       |string         |이용자가 원하는 닉네임
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: 실패 - update_00
 *              |message        |string         |실패 사유
 *              |data           |json           |
 *              ||uid_u         |string         |이용자의 고유값
 *              ||nickname      |string         |최종적으로 적용된 닉네임
 * desc:        계정의 닉네임을 변경함
 *              이때 이름에 이모지나 특수문자 등이 혼합되면 모두 걸러냄
 *              이름의 앞이나 뒤에 공백 문자가 들어갈시 그것도 걸러냄
 */
```

### 게스트 회원가입 & 로그인

```fold
/* desc:	게스트로 회원가입 및 로그인
 * method:	post
 * url:		<http://$>{host}:52531/guest_login
 *		|name		|type		|desc
 * input: 	|uid_u		|string		|이용자의 고유값
 * output:	|code	 	|int		|0: 가입 및 로그인 성공, 1: 실패 - select_00, 2: 실패 - insert_00, 3: 실패 - select_01
 *		|data	 	|json		|
 *		||uid		|string		|계정 고유값
 *		||email		|string		|계정 이메일
 *		||nickname	|string		|닉네임
 *		||gold		|int		|소지 골드
 *		||cash		|int		|소지 캐시
 *		||home_max	|int		|캐터리 최대 보관수
 *		||type		|int		|0: 구글 로그인, 1: 이메일 로그인
 *		||level		|int		|계정의 레벨
 *		||exp		|int		|계정의 경험치
 *		||point		|int		|계정의 잔여 스킬 포인트
 *		||skill		|array int	|계정의 스킬 레벨 배열
 *		||correction	|array int	|계정의 스킬 레벨 보정치 배열
 *		|message	|string		|반환 메세지
 * desc:	게스트 uid 를 클라이언트에서 생성
 *		이후 해당 uid를 이용해 회원가입 및 서버 접속
 *		게스트 계정의 서버상 type은 3이지만 클라에서 별도로 관리해도 무방
 */
```

### 로컬라이징된 텍스트 받아오기

```fold
/* desc:	로컬라이징을 위한 모든 데이터의 획득
 * method:	post
 * url:		<http://$>{host}:52531/get_local
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||name		|string		|설정창에 보일 글자
 *		||code		|string		|표준 국가 코드(2글자 버전)
 *		||data		|array string	|스프레드 시트의 넘버링에 대응하는 번역 문자열
 * desc:	로컬라이징에 사용되는 모든 문자열을 반환 받음
 *		각 국가 코드와 나의 국가 코드를 이용해 대응되는 문자열들을 이용하면 됨
 *		현재 KR(한국), US(미국), JP(일본(한자)), JP1(일본(가나))에 대응 가능
 */

```

### 국가코드 획득

```fold
/* desc:	국가 코드를 획득
 * method:	post
 * url:		<http://$>{host}:52531/get_country
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패
 *		|message	|string		|실패 사유
 *		|data		|string		|표준 국가 코드(2글자 버전)
 * desc:	로컬라이징을 수행하기 위한 국가 코드를 획득
 *		현재 KR(한국), US(미국), JP(일본(한자)), JP1(일본(가나))에 대응 가능
 *		기본적으로 어디에도 속하지 않으면 US를 반환
 */
```

### 게시판 가져오기v2

```fold
/* desc:	게시판 가져오기
 * method:	post
 * url:		<http://$>{host}:52532/get_boards_v2
 *		|name		|type		|desc
 * input:	|type		|int		|게시판의 종류
 *		|count		|int		|가져오는 게시물의 수
 *              |code_c         |string         |표준 국가 코드(2글자 버전)
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 게시물 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||title		|string		|게시물의 제목
 *		||content	|string		|게시판의 본문
 *		||create_at	|string		|게시물이 작성된 일시
 * desc:	게시판에 저장된 게시물을 호출
 *		이때, 게시물은 가장 최근 생성된 것을 기준으로 내림차순 정렬됨
 *		제목 및 내용물에 길이 제한은 없음
 *		각 텍스트의 호출이 실제로 잘되는지 확인은 필요함
 *		국가 코드는 현재 US가 기본값으로 되어 있음
 *		서버 상에서 내부적으로 JP와 JP1은 동일하게 JP로 취급함
 */
```

### ~~시즌 보상 정보와 내 상위 등급 가져오기~~ 대체됨-2023-10-18

```fold
/* desc:	이번 시즌에서 달성한 입장(?) 정보 가져오기
 * method:	post
 * url:		<http://$>{host}:52532/get_season_rank
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공 혹은 개인 랭킹 없음, 1: 실패 - select_00, 2: 실패 - 현재 시즌 없음, 3: 실패 - select_01, 4: 실패 - 랭킹 정보 없음, 5: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||ranking	|int		|이번 시즌 순위
 *		||uid_u		|string		|이용자의 고유값
 *		||nickname	|string		|이용자의 닉네임
 *		||percent	|float		|이번 시즌 순위 백분율
 *		||reward	|int		|현재 순위 기준 보상
 *		||rewards	|array_json	|현재 시즌 보상 목록
 *		|||percent	|int		|상위 X 퍼센트
 *		|||reward	|int		|대응되는 보상의 개수
 *		||begin_at	|string		|시작 일시
 *		||end_at	|string		|종료 일시
 *		||name		|string		|시즌 이름, 숫자일 수도 있고 문자일 수도 있고
 * desc:	이번 시즌에서, 현재 시점으로, 받을 수 있는 보상 등을 반환
 */
```

### 고양이의 보너스 스탯 등 추가정보 가져오기

```fold
/* desc:	캐릭터의 각종 추가 정보를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_cat_bonus
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공 혹은 개인 랭킹 없음, 1: 실패 - select_00, 2: 실패 - 그런 캐릭터 없음
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||status	|int		|1: 코네코, 2: 코이네코, 상태에 따라 성장 게이지 표시 판단
 *		||action_remain	|int		|코네코일 경우 진화를 위해 필요한 추가 돌보기 기능 횟수
 *		||action_max	|int		|코네코일 경우 진화를 위해 필요한 돌보기 기능 필요치
 *		||stat_bonus	|int		|모든 스탯 보너스 비율(0 %, 25 %, 50 %, 75 %)
 *		||stat_avg	|int		|욕구 수치의 평균
 * desc:	진화는 코네코일 경우에만 표시
 *		게이지는 최대 28의 수치를 가질 수 있음
 *		만약 action_remain이 5라면 23만큼 채워질 것
 *		욕구에 따른 보너스 스탯은 (int(욕구 평균 / 25) - 1) * 25 과 동일
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>계정 관련</span>

### 유저 로그인 V3

```fold
/* desc:	계정 정보를 이용해 로그인
 * method:	post
 * url:		http://${host}:52531/user_login_v3
 *		|name		|type		|desc
 * input:       |email		|string		|메일 주소
 *		|type		|int		|0: 구글 로그인, 1: 이메일 로그인, 2: 애플 로그인, 3: 게스트 로그인
 *		|password       |string		|비밀번호, 구글 로그인일 시 없어도 됨
 *		|uid_m		|string		|기기의 고유값
 *		|is_auto	|int		|0: 자동 로그인 아님, 1: 자동 로그인임
 * output:	|code		|int		|0: 가입 및 로그인 성공, 1: 이메일 조회 실패, 2: 비밀번호 틀림, 3: 아이디 생성 실패, 4: 계정 생성 결과 조>회 실패, 5: 구글 로그인시 계정 생성 및 로그인 성공
 *		|data		|json		|
 *		||uid		|string		|계정 고유값
 *		||email		|string		|계정 이메일
 *		||nickname	|string		|닉네임
 *		||gold		|int		|소지 골드
 *		||cash		|int		|소지 캐시
 *		||home_max	|int		|캐터리 최대 보관수
 *		||egg_max	|int		|알 보유 가능 최대 개수
 *		||type		|int		|0: 구글 로그인, 1: 이메일 로그인
 *		||level		|int		|계정의 레벨
 *		||exp		|int		|계정의 경험치
 *		||point		|int		|계정의 잔여 스킬 포인트
 *		||skill		|array int	|계정의 스킬 레벨 배열
 *		||correction	|array int	|계정의 스킬 레벨 보정치 배열
 *		|message	|string		|반환 메세지
 */
```

### 닉네임 변경 V2

```fold
/* desc:	계정의 닉네임을 변경
 * method:	post
 * url:		http://${host}:52532/set_nickname_v2
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|nickname	|string		|이용자가 원하는 닉네임
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - select_01, 3: 실패 - 닉네임 이미 존재, 4: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_u		|string		|이용자의 고유값
 *		||nickname	|string		|최종적으로 적용된 닉네임
 * desc:	계정의 닉네임을 변경함
 *		단, 변경하고자하는 닉네임이 중복되는지에 대한 여부를 확인
 *		만약 중복되는 닉네임(특수문자 및 이모지 등 모두 제외된 상태)을 요청했다면 에러 반환
 */
```

### 인증코드 확인 및 계정 생성

```fold
/* desc:	인증코드 확인 및 해당하는 계정을 생성
 * method:	post
 * url:		http://${host}:52531/auth_v2
 *		|name		|type		|desc
 * input:	|email		|string		|메일 주소
 *		|acode		|string		|인증 코드
 *		|password	|string		|비밀번호
 * output:	|code		|int		|0: 성공, 1: 인증 실패, 2: 계정 생성 실패, 3: 계정 존재
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uuid		|string		|가입 승인된 uuid
 *		||email		|string		|가입 승인된 email
 * desc:	기저장된 인증 데이터를 갱신하고 가입에 사용된 데이터 및 uuid를 반환
 */
```

### 미니게임에 사용되는 스킬의 레벨 및 증감치를 가져오기 V2

```fold
/* desc:	미니게임에 사용되는 스킬의 레벨 및 증감치를 가져오기
 * method:	post
 * url:		http://${host}:52532/get_run_skill_v2
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - select_01
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||arr_merge	|array int	|계정 및 캐릭터의 스킬 레벨 합산 배열
 *		||arr_value	|array int	|최종 스킬 증감치 배열
 * desc:	캐릭터 스킬 레벨 + 계정 스킬 레벨 + 돌보기 스킬 레벨의 합산을 반환
 *		만약 캐릭터가 아직 유년기 상태라면 스킬 레벨은 절반(버림 연산)만 가산됨
 *		각 스킬은 레벨 1당 2%의 증감치를 적용
 *		각 스킬의 레벨 최대치는 모두 100으로 동일, 즉 최대 증감치는 200%
 */
```

### 로그인을 한 이력이 있는지 확인하고 해당값을 반환

```fold
/* desc:	로그인을 한 이력이 있는지 확인하고 해당값을 반환
 * method:	post
 * url:		<http://$>{host}:52531/get_is_auto
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 *		|uid_m		|string		|기기 고유값
 * output:	|code		|int		|0: 성공
 *		|message	|string		|상황 고지
 *		|data		|json		|-
 *		||is_auto	|int		|0: 이력 없음, 1: 이력 있음
 * desc:	1주일 안에 로그인을 하면 갱신되는 자동 로그인 내역 조회
 *		뭐가 어찌됐건 로그인을 하면 1주일 동안 로그인 이력이 저장됨
 *		기기 고유값은 클라이언트를 최초에 실행할 때 만들어두고 보내주면 됨
 */
```

## ----------------------------------------------

## <span style='color:#8854d0'>고양이 관리 관련</span>

### 새 고양이의 탄생 V2

```fold
/* desc:	새 고양이의 탄생
 * method:	post
 * url:		http://${host}:52532/get_cat_new_v2
 *		|name		|type		|desc
 * input:	|uid		|string		|이용자 고유값
 *		|cat_status	|int		|0: 알 받기, 1: 유기묘 받기
 *		|uid_c_dad	|string		|아빠 고양이의 uid, seed 받기라면 없어도 됨
 *		|uid_c_mom	|string		|엄마 고양이의 uid, seed 받기라면 없어도 됨
 * output:	|code		|int		|0: 성공, 1: 실패 - insert_00, 2: 실패 - insert_01, 3: 실패 - select_00
 *		|message 	|string		|실패 사유
 *		|data	 	|json		|
 *		||uid		|string		|고양이의 uid
 *		||uid_u		|string		|현재 주인의 uid
 *		||uid_c_dad	|string		|아빠 고양이의 uid, seed 고양이일때 null
 *		||uid_c_mom	|string		|엄마 고양이의 uid, seed 고양이일때 null
 *		||date_cur	|int		|고양이의 잔여 교배 횟수
 *		||date_max	|int		|고양이의 최대 교배 횟수
 *		||name		|string		|고양이의 이름
 *		||stat_v2	|array		|캐터리에서의 상태값_v2
 *		||status	|int		|0: 알, 1: 유년, 2: 성년, 3: NFT
 *		||is_seed	|int		|0: seed 아님, 1: seed 맞음
 * desc:	새로운 고양이를 창출
 *		생성되는 고양이는 상태에 따라 유아 및 그 외로 구분됨
 *		유기묘를 받는다면 부모의 uid는 없어도 되며 cat_status는 1
 *		교배결과인 알을 받는다면 부모의 uid가 필수이며 cat_status는 0
 *		stat_v2 는 기존의 5개짜리 stat을 대체하기 위해 추가 및 변경됨
 */
```

### 캐릭터의 각종 추가 정보를 획득 V2

```fold
/* desc:	캐릭터의 각종 추가 정보를 획득
 * method:	post
 * url:		http://${host}:52532/get_cat_bonus_v2
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||status	|int		|1: 코네코, 2: 코이네코, 상태에 따라 성장 게이지 표시 판단
 *		||action_remain	|int		|코네코일 경우 진화를 위해 필요한 추가 돌보기 기능 횟수
 *		||action_max	|int		|코네코일 경우 진화를 위해 필요한 돌보기 기능 필요치
 * desc:	v2는 진화에 관련된 요소들만 반환
 *		진화는 코네코일 경우에만 표시
 *		게이지는 최대 28의 수치를 가질 수 있음
 *		만약 action_remain이 5라면 23만큼 채워질 것
 */
```

### 캐릭터의 실시간 능력치를 가져오기

```fold
/* desc:	캐릭터의 실시간 능력치를 가져오기
 * method:	post
 * url:		http://${host}:52532/get_cat_stat_v2
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message	|string		|반환 메세지
 *		|data		|json		|
 *		||arr_skill_c	|array int	|캐릭터 능력치
 *		||arr_skill_u	|array int	|이용자 능력치
 *		||arr_skill_p	|array int	|돌보기 능력치
 *		||arr_skill_m	|array int	|능력치 총합
 *		||arr_skill_v	|array int	|실제 반영되는 능력치
 * desc:	캐릭터의 현재 능력치를 호출
 *		단, 캐릭터가 아직 유아체라면 모든 능력치는 절반으로 감산되어 전달됨
 *		때문에 유아체의 능력치는 아무리 높아도 50을 넘길 수 없음
 *		이는 계정 스킬 레벨에도 동일하게 적용됨
 */
```

### 선택한 욕구 게이지를 만땅으로 채움

```fold
/* desc:	선택한 욕구 게이지를 만땅으로 채움
 * method:	post
 * url:		http://${host}:52532/set_fast_care_v2
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 *		|i_des		|int		|0 ~ 5 욕구 게이지의 인덱스
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00 failed, 2: 실패 - select_01, 3: 실패 - select_02, 4: 실패 - 젤리 부족, 5: 실패 - 이미 만땅, 6: 실패 - update_00, 7: 실패 - update_01
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cash_left	|int		|남은 젤리
 *		||arr_skill_c	|array int	|캐릭터 능력치
 *		||arr_skill_u	|array int	|이용자 능력치
 *		||arr_skill_p	|array int	|돌보기 능력치(실제로 변하는 값)
 *		||arr_skill_m	|array int	|능력치 총합
 * desc:	선택한 스탯 게이지를 최대치로 채움
 *		단, 스탯 게이지의 수치가 99 이하일 때만 호출 가능
 *		차감되는 젤리의 수는 데이터베이스의 common 17번에 저장됨
 *		v2 부터 게이지의 수가 6개로 늘어남에 따라 동일하게 반영됨
 *		유아체인 경우 각 능력치의 값은 버림 연산 기준으로 절반이 됨
 */
```

### 다마고치 액션 및 그에 따른 변경점 가져오기

```fold
/* desc:	다마고치 액션 및 그에 따른 변경점 가져오기
 * method:	post
 * url:		http://${host}:52532/set_home_action_v2
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 *		|num_action	|int		|액션의 배열 번호(0~5)
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - select_01, 3: 실패 - select_02, 4: 실패 - 골드 부족, 5: 실패 - update_00, 6: 실패 - 이미 꽉참, 7: 실패 - update_01
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||uid_u		|string		|이용자의 고유값
 *		||uid_c		|string		|캐릭터의 고유값
 *		||now_gold	|int		|이제 남은 골드
 *		||gold_action	|int		|액션을 수행하는데 소모한 골드
 *		||arr_skill_c	|array int	|캐릭터 능력치
 *		||arr_skill_u	|array int	|이용자 능력치
 *		||arr_skill_p	|array int	|돌보기 능력치(실제로 변하는 값)
 *		||arr_skill_m	|array int	|능력치 총합
 *		||evolve_left	|int		|상호작용을 한 이후 진화까지 남은 시간(초)
 * desc:	다마고치에서 액션을 수행하고, 그 결과를 반환
 *		각 액션마다 소모되는 재화 이상의 재화를 보유하고 있어야만 함
 *		지출한 골드 및 계정에 남은 골드를 반환하며, 캐릭터의 마다고치상 능력치 배열을 반환
 *		캐릭터 + 이용자 + 돌보기 능력치의 합은 100을 넘길 수 없음
 *		진화는 유아체만 가능하며 한번의 액션당 6시간씩 감소함
 *		반환되는 evolve_left의 값은 이미 진화했을 시 음수를, 아직 진화하지 않았다면 양수를 반환
 */
```

## ----------------------------------------------

## <span style='color:#8854d0'>런게임 관련</span>

### 런 게임 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감

```fold
/* desc:	[런 게임] 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감
 * method:	post
 * url:		<http://$>{host}:52534/set_resurrect
 *		|name		|type		|desc
 * input:	|is_adv		|int		|광고 부활 여부
 *		|uid_g		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - select_01, 4: 실패 - 공용 데이터 없음, 5: 실패 - update_00, 6: 실패 - update_01, 7: 실패 - 더 이상 부활 불가, 8: 실패 - 돈 없음 혹은 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cost		|int		|부활에 사용된 비용
 *		||count		|int		|누적 부활 횟수
 * desc:	게임 중 부활 기능을 사용하고 데이터를 갱신
 *		common 데이터는 18 번을 사용, 현재 형태는 이맇게 됨 ["20","40","80","160"]
 *		반환되는 count는 이번 부활을 성공한 결과를 포함
 *		광고를 봐서 부활한다면 is_adv 값을 1로 보내주면 됨
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>두들점프 관련 ⇒ 포트 다름</span>

### 시즌 보상 정보와 내 상위 등급 가져오기(두들)

```fold
/* desc:	이번 시즌에서 달성한 입장(?) 정보 가져오기
 * method:	post
 * url:		<http://$>{host}:52532/get_season_rank_doodle
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공 혹은 개인 랭킹 없음, 1: 실패 - select_00, 2: 실패 - 현재 시즌 없음, 3: 실패 - select_01, 4: 실패 - 랭킹 정보 없음, 5: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|array array_json|
 *		||ranking	|int		|이번 시즌 순위
 *		||uid_u		|string		|이용자의 고유값
 *		||nickname	|string		|이용자의 닉네임
 *		||percent	|float		|이번 시즌 순위 백분율
 *		||reward	|int		|현재 순위 기준 보상
 *		||rewards	|array_json	|현재 시즌 보상 목록
 *		|||percent	|int		|상위 X 퍼센트
 *		|||reward	|int		|대응되는 보상의 개수
 *		||begin_at	|string		|시작 일시
 *		||end_at	|string		|종료 일시
 *		||name		|string		|시즌 이름, 숫자일 수도 있고 문자일 수도 있고
 * desc:	이번 시즌에서, 현재 시점으로, 받을 수 있는 보상 등을 반환
 */
```

### 시즌 스테이지를 시작하고 스테이지 정보 가져오기(두들)

```fold
/* desc:	시즌 스테이지를 시작하고 스테이지 정보 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52537/set_season_begin>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 시즌 시드값 없음, 3: 실패 - select_01, 4: 실패 - 그런 캐릭터 없음
, 5: 실패 - insert_00, 6: 실패 - 세션 이미 존재
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||stage		|array string	|스테이지를 구성하는 숫자(문자열)의 배열
 *		||seed		|int		|스테이지를 생성하는데 사용된 seed 값
 *		||uid_s		|int		|시즌의 고유값
 *		||uid_g		|int		|게임의 고유값
 *		||uid_u		|int		|이용자의 고유값
 *		||uid_c		|int		|캐릭터의 고유값
 * desc:	고양이의 정보를 받아 새로운 게임을 생성
 *		시즌 게임에 대한 시작만을 담당
 *		현재 시즌에 따라 총 1024 개의 스테이지 배열을 반환
 *		3월 이후부터 시드값이 바뀔 예정이므로 스테이지 구성이 변경될 것
 */
```

### 스테이지를 진행하고 있는 중간중간 진행 정보 저장하기(두들)

```fold
/* desc:	스테이지를 진행하고 있는 중간중간 진행 정보 저장하기
 * method:	post
 * url:		<http://54.180.106.167:52537/set_game_mid>
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 * desc:	스테이지 진행 중간마다 플레이 기록을 저장하고 게임의 정상 진행 여부를 반환
 *		현재 거리 1000, 골드 1000, 캐시 100 이상 차이날 때, 및 각각 차이가 0일 때 오류(3) 반환
 */
```

### 러닝 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기(두들)

```fold
/* desc:	러닝 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기
 * method:	post
 * url:		<http://54.180.106.167:52537/set_game_end>
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||get_exp	|int		|경험치
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|10위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||now		|json		|이번 게임 기록
 *		|||is_season	|int		|0: 비시즌, 1: 시즌
 *		|||dist		|int		|도달 거리
 *		|||gold		|int		|획득 골드
 *		|||cash		|int		|획득 캐시
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||name		|string		|캐릭터의 닉네임
 * desc:	게임을 종료하고 필요한 값을 반환
 *		rank 는 내가 달성했던 기록중 가장 랭킹이 높은 게임 기록
 *		ranking 은 서버상 존재하는 가장 랭킹이 높은 10개의 게임 기록 배열
 *		now 는 이번 게임에서 달성한 기록
 */
```

### 게임에서의 탈주(시즌, 비시즌 공용)(두들)

```fold
/* desc:	게임에서의 탈주(시즌, 비시즌 공용)
 * method:	post
 * url:		<http://54.180.106.167:52537/set_game_escape>
 *		|name		|type		|desc
 * input:	|uid_c		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|-		|-
 * desc:	달리기 게임 도중 일시정지를 누르고 탈주할 때 등에 사용
 *		정상 탈주 여부는 code를 통해 확인하며 0일 때만 동작한다고 보면 됨
 *		하지만 어차피 탈주가 목적인데다 세션이 2분 지속되므로 실패해도 에러 메세지를 띄우고 탈주하면 될 듯
 */
```

### 캐터리에서 두들랭킹 불러오기

```fold
/* desc:	리더 보드 정보를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_game_ranks_doodle
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|is_season	|int		|0: 비시즌, 1: 시즌
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 시즌 없음, 3: 실패 - select_01, 4: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|50위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|string		|1: 유아체, 2: 성체
 * desc:	내 이용자 고유값과 시즌 여부를 통해 해당하는 리더 보드를 호출
 *		리더보드는 나의 최고 기록을 포함하지만 정보가 없다면 각각 빈 배열로 반환될 것
 */
```

### 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감

```fold
/* desc:	[두들 게임] 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감
 * method:	post
 * url:		<http://$>{host}:52537/set_resurrect
 *		|name		|type		|desc
 * input:	|is_adv		|int		|광고 부활 여부
 *		|uid_g		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - select_01, 4: 실패 - 공용 데이터 없음, 5: 실패 - update_00, 6: 실패 - update_01, 7: 실패 - 더 이상 부활 불가, 8: 실패 - 돈 없음 혹은 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cost		|int		|부활에 사용된 비용
 *		||count		|int		|누적 부활 횟수
 * desc:	게임 중 부활 기능을 사용하고 데이터를 갱신
 *		common 데이터는 18 번을 사용하며, 현재 형태는 이맇게 됨 ["20","40","80","160"]
 *		반환되는 count는 이번 부활을 성공한 결과를 포함
 *		광고를 봐서 부활한다면 is_adv 값을 1로 보내주면 됨
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>우편기능</span>

### 이용자의 모든 우편을 검색 및 반환

```fold
/* desc:	이용자의 모든 우편을 검색 및 반환
 * method:	post
 * url:		<http://$>{host}:52531/get_posts
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - session 서버 오류
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||count		|int		|우편물 개수
 *		||posts		|array json	|우편물
 *		||unread	|int		|0: 안 읽은거 없음, 1: 안 읽은거 있음
 *		|||uid_p	|string		|우편물의 고유값
 *		|||type		|int		|0: 시즌 보상, 1: 점검 공지, 2: 장애 공지, ...
 *		|||is_read	|int		|0: 안 읽음, 1: 읽음
 *		|||delete_at	|int		|timestamp 삭제 일시(초)
 *		|||reward_type	|int		|0: 젤리, 1: 코인, ...
 *		|||reward_count	|int		|보상의 개수
 *		|||create_at	|string		|우편 생성 날짜
 *		|||sec_remain	|int		|우편 유효 시간(초)
 * desc:	이용자의 고유값을 통해 받은 모든 우편물을 조회
 *		현재 각 우편의 유효기간은 7일
 */
```

### 이용자의 우편을 읽음 처리

```fold
/* desc:	이용자의 우편을 읽음 처리
 * method:	post
 * url:		<http://$>{host}:52531/set_post_read
 *		|name		|type		|desc
 * input:	|uid_p		|string		|우편물의 고유값
 * output:	|code		|int		|0: 성공, 1: 실채 - 그런 우편 없음, 2: 실패 - session 서버 오류
 *		|message	|string		|실패 사유
 *		|data		|json		|아무것도 없음
 * desc:	잘 처리됐으면 0, 아니면 1
 */
```

### 이용자의 우편을 읽음 처리 V2

```fold
/* desc:        이용자의 우편을 읽음 처리
 * method:      post
 * url:         http://${host}:52531/set_post_read_v2
 *              |name           |type           |desc
 * input:       |uid_p          |string         |우편물의 고유값
 * output:      |code           |int            |0: 성공, 1: 실패 - 그런 우편 없음, 2: 실패 - update_00, 3: 실패 - 그런 우편 없음
 *              |message        |string         |실패 사유
 *              |data           |json           |
 *		||type		|int		|0: 시즌 보상, 1: 점검 보상, etc...
 *		||reward_type	|int		|0: 젤리, 1: 코인
 *		||reward_count	|int		|지급된 보상의 개수
 * desc:        보상을 받아야만 읽음처리가 됨
 *		보상을 받았다면 우편에 국왕의 도장을 쾅! 찍어줌
 *		만약 보상을 받지 않았다면 우편함에 항상 떠있을 것
 *		통상적인 우편의 유효기간은 배포된 시점을 기준으로 1주일
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>편의성 현질</span>

### 즉시 부화를 실행하고 남은 젤리를 반환

```fold
/* desc:	즉시 부화를 실행하고 남은 젤리를 반환
 * method:	post
 * url:		<http://$>{host}:52532/set_fast_hatch
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실채 - select_00 failed, 2: 실패 - 그런 인큐 없음, 3: 실패 - select_01, 4: 실패 - 그런 이용자 없음, 5: 실패 - select_02, 6: 실패 - 공용 데이터 없음, 7: 실패 - 젤리 부족, 8: 실패 - update_00, 9: 실패 - update_01
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cash_left	|int		|남은 젤리
 * desc:	캐릭터를 즉시 부화할 수 있도록 진화 시간을 현재 시간으로 변경
 *		젤리는 모든 검증 작업 이후에 차감
 *		차감되는 젤리의 수는 데이터베이스의 common 16번에 저장됨
 */
```

### 선택한 욕구 게이지(90 이하의)를 만땅으로 채움

```fold
/* desc:	선택한 욕구 게이지(90 이하의)를 만땅으로 채움
 * method:	post
 * url:		<http://$>{host}:52532/set_fast_care
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 *		|i_des		|int		|0 ~ 4 욕구 게이지의 인덱스
 * output:	|code		|int		|0: 성공, 1: 실채 - select_00 failed, 2: 실패 - 그런 캐릭터 없음, 3: 실패 - 90 초과함, 4: 실패 - select_01, 5: 실패 - 공용 데이터 없음, 6: 실패 - select_02, 7: 실패 - 그런 이용자 없음, 8: 실패 - 젤리 부족, 9: 실패 - update_00, 10: 실패 - update_01
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cash_left	|int		|남은 젤리
 *		||stat		|array int	|욕구 게이지 배열
 * desc:	선택한 욕구 게이지를 최대치로 채움
 *		단, 욕구 게이지의 수치가 90 이하일 때만 호출 가능
 *		차감되는 젤리의 수는 데이터베이스의 common 17번에 저장됨
 */
```

### 광고 보고 부화시간 1시간 단축

```fold
/* desc:	광고를 보면 부화에 필요한 시간을 1시간 감소시킴
 * method:	post
 * url:		<http://$>{host}:52532/set_incu_ad
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 *		|uid_i		|string		|부화기 고유값
 *		|uid_c		|string		|캐릭터 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 부화기(이용자, 캐릭터) 없음, 3: 실패 - update_00
 *		|message	|string		|상황 고지
 *		|data		|json		|-
 * desc:	광고 1회당 부화 필요 시간을 1시간씩 감소시킴
 */
```

### 무료 캐시가 있는지 조회

```fold
/* desc:	상점에서 획득 가능한 무료 캐시가 있는지 조회
 * method:	post
 * url:		<http://$>{host}:52532/get_shop_free
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - session error
 *		|message	|string		|상황 고지
 *		|data		|json		|-
 *		||is_able	|int		|0: 못 받음, 1: 받을 수 있음
 *		||sec_remain	|int		|무료 캐시를 받기 위해 남은 시간
 * desc:	무료로 캐시를 획득할 수 있는지 여부를 조회함
 *		받을 수 있다면 {is_able: 1, sec_remain: 0}을 반환
 *		받을 수 없다면 {is_able: 0, sec_remain: 0초과}를 반환
 */
```

### 무료 캐시를 획득하고 3시간 세션 설정

```fold
/* desc:	상점에서 무료 캐시를 획득하고 3시간 세션 설정
 * method:	post
 * url:		<http://$>{host}:52532/set_shop_free
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - session error, 3: 실패 - update_00, 4: 세션 아직 있는데?
 *		|message	|string		|상황 고지
 *		|data		|json		|-
 *		||sec_remain	|int		|무료 캐시를 받기 위해 남은 시간
 *		||cash		|int		|획득한 캐시의 수
 * desc:	무료로 캐시를 획득하고 서버에 세션 데이터를 남김
 *		세션은 현재 3시간 유지되므로 sec_remain의 최댓값은 10800
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>쿠폰 관련</span>

### 쿠폰 그룹의 인덱스를 입력 받고 복수의 쿠폰을 발급받음

```fold
/* desc:	쿠폰 그룹의 인덱스를 입력 받고 복수의 쿠폰을 발급받음
 * method:	post
 * url:		<http://$>{host}:52538/get_coupons
 *		|name		|type		|desc
 * input:	|index		|int		|쿠폰 그룹의 고유값
 *		|count		|int		|발급 받을 쿠폰의 수
 * output:	|code		|int		|0: 성공
 *		|message	|string		|상황 고지
 *		|data		|arr_string	|쿠폰 배열
 * desc:	쿠폰 그룹의 인덱스를 입력 받고 해당하는 쿠폰을 발급
 *		한번에 발급 받는 쿠폰의 수에 제한은 없으나 아래는 유의
 *		쿠폰 그룹 인덱스의 최대값은 0xFF = 255
 *		각 그룹의 쿠폰 최대 수는 0xFFFF = 65535
 *		부화기는 하나의 쿠폰에 하나만 포함 가능
 */
```

### 쿠폰 그룹의 인덱스를 입력 받고 하나의 쿠폰을 발급받음

```fold
/* desc:	쿠폰 그룹의 인덱스를 입력 받고 하나의 쿠폰을 발급받음
 * method:	post
 * url:		<http://$>{host}:52538/get_coupon
 *		|name		|type		|desc
 * input:	|index		|int		|쿠폰 그룹의 고유값
 * output:	|code		|int		|0: 성공
 *		|message	|string		|상황 고지
 *		|data		|string		|쿠폰
 * desc:	쿠폰 그룹의 인덱스를 입력 받고 해당하는 쿠폰을 발급
 *		쿠폰 그룹 인덱스의 최대값은 0xFF = 255
 *		각 그룹의 쿠폰 최대 수는 0xFFFF = 65535
 *		부화기는 하나의 쿠폰에 하나만 포함 가능
 */
```

### 발급받은 쿠폰을 사용처리하고 해당하는 보상을 지급

```fold
/* desc:	발급받은 쿠폰을 사용처리하고 해당하는 보상을 지급
 * method:	post
 * url:		<http://$>{host}:52538/set_coupon
 *		|name		|type		|desc
 * input:	|coupon		|string		|쿠폰 시리얼
 *		|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - 쿠폰 검증, 2: 실패 - 이미 사용, 3: 실패 - 그런 쿠폰 없음, 4: 실패 - update_00, 5: 실패 - 보상 지급(쿠폰 미사용), 6: 실패 - 그냥 쿠폰 터짐
 *		|message	|string		|상황 고지
 *		|data		|string		|쿠폰
 *		||gold		|int		|지급된 골드의 개수(지급 안될 시 0)
 *		||cash		|int		|지급된 캐시의 개수(지급 안될 시 0)
 *		||incu		|int		|지급된 부화기의 개수(현재 한개만 가능)(지급 안될 시 0)
 * desc:	발급받은 쿠폰을 사용했다고 인정
 *		쿠폰 그룹 내에서는 한명이 하나의 쿠폰을 사용할 수 있음
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>네코팡</span>

### 시즌 스테이지를 시작하고 스테이지 정보 가져오기

```fold
/* desc:        시즌 스테이지를 시작하고 스테이지 정보 가져오기
 * method:      post
 * url:         <http://$>{host}:52540/set_season_begin
 *              |name           |type           |desc
 * input:       |uid_c          |string         |캐릭터의 고유값
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 시즌 시드값 없음, 3: 실패 - select_01, 4: 실패 - 그런 캐릭터 없음
, 5: 실패 - insert_00, 6: 실패 - 세션 이미 존재
 *              |message        |string         |실패 사유
 *              |data           |               |
 *              ||stage         |array string   |스테이지를 구성하는 숫자(문자열)의 배열
 *              ||seed          |int            |스테이지를 생성하는데 사용된 seed 값
 *              ||uid_s         |int            |시즌의 고유값
 *              ||uid_g         |int            |게임의 고유값
 *              ||uid_u         |int            |이용자의 고유값
 *              ||uid_c         |int            |캐릭터의 고유값
 * desc:        고양이의 정보를 받아 새로운 게임을 생성
 *              시즌 게임에 대한 시작만을 담당
 *              현재 시즌에 따라 총 1024 개의 스테이지 배열을 반환
 *              3월 이후부터 시드값이 바뀔 예정이므로 스테이지 구성이 변경될 것
 */
```

### 스테이지를 진행하고 있는 중간중간 진행 정보 저장하기

```fold
/* desc:        스테이지를 진행하고 있는 중간중간 진행 정보 저장하기
 * method:      post
 * url:         <http://$>{host}:52540/set_game_mid
 *              |name           |type           |desc
 * input:       |uid_g          |string         |게임의 고유값
 *              |gold           |int            |현재까지 획득한 전체 골드
 *              |cash           |int            |현재까지 획득한 전체 캐시
 *              |dist           |int            |현재까지 진행한 전체 거리
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *              |message        |string         |실패 사유
 * desc:        스테이지 진행 중간마다 플레이 기록을 저장하고 게임의 정상 진행 여부를 반환
 *              현재 거리 1000, 골드 1000, 캐시 100 이상 차이날 때, 및 각각 차이가 0일 때 오류(3) 반환
 */
```

### 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기

```fold
/* desc:        게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기
 * method:      post
 * url:         <http://$>{host}:52540/set_game_end
 *              |name           |type           |desc
 * input:       |uid_g          |string         |게임의 고유값
 *              |gold           |int            |현재까지 획득한 전체 골드
 *              |cash           |int            |현재까지 획득한 전체 캐시
 *              |dist           |int            |현재까지 진행한 전체 거리
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *              |message        |string         |실패 사유
 *              |data           |               |
 *              ||get_exp       |int            |경험치
 *              ||rank          |json           |내 랭킹 정보
 *              |||ranking      |int            |내 랭킹
 *              |||uid_u        |string         |이용자의 고유값
 *              |||uid_c        |string         |캐릭터의 고유값
 *              |||nickname     |string         |이용자의 닉네임
 *              |||level        |string         |이용자의 레벨
 *              |||name         |string         |캐릭터의 닉네임
 *              |||max_dist     |int            |도달 거리
 *              |||status       |int            |1: 유아체, 2: 성체
 *              ||ranks         |array json     |10위까지의 랭킹 정보
 *              |||ranking      |int            |순위
 *              |||uid_u        |string         |이용자의 고유값
 *              |||uid_c        |string         |캐릭터의 고유값
 *              |||nickname     |string         |이용자의 닉네임
 *              |||level        |int            |이용자의 레벨
 *              |||name         |string         |캐릭터의 닉네임
 *              |||max_dist     |string         |도달 거리
 *              |||status       |int            |1: 유아체, 2: 성체
 *              ||now           |json           |이번 게임 기록
 *              |||is_season    |int            |0: 비시즌, 1: 시즌
 *              |||dist         |int            |도달 거리
 *              |||gold         |int            |획득 골드
 *              |||cash         |int            |획득 캐시
 *              |||uid_c        |string         |캐릭터의 고유값
 *              |||name         |string         |캐릭터의 닉네임
 * desc:        게임을 종료하고 필요한 값을 반환
 *              rank 는 내가 달성했던 기록중 가장 랭킹이 높은 게임 기록
 *              ranking 은 서버상 존재하는 가장 랭킹이 높은 10개의 게임 기록 배열
 *              now 는 이번 게임에서 달성한 기록
 */
```

### 게임에서의 탈주(시즌, 비시즌 공용)

```fold
/* desc:        게임에서의 탈주(시즌, 비시즌 공용)
 * method:      post
 * url:         <http://$>{host}:52540/set_game_escape
 *              |name           |type           |desc
 * input:       |uid_c          |string         |게임의 고유값
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 세션 없음
 *              |message        |string         |실패 사유
 *              |data           |-              |-
 * desc:        달리기 게임 도중 일시정지를 누르고 탈주할 때 등에 사용
 *              정상 탈주 여부는 code를 통해 확인하며 0일 때만 동작한다고 보면 됨
 *              하지만 어차피 탈주가 목적인데다 세션이 2분 지속되므로 실패해도 에러 메세지를 띄우고 탈주하면 될 듯
 */
```

### 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감

```fold
/* desc:        게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감
 * method:      post
 * url:         <http://$>{host}:52540/set_resurrect
 *              |name           |type           |desc
 * input:       |is_adv         |int            |광고 부활 여부
 *              |uid_g          |string         |게임의 고유값
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - select_01, 4: 실패 - 공용 데이터 없음, 5: 실패 - update_00, 6: 실패 - update_01, 7: 실패 - 더 이상 부활 불가, 8: 실패 - 돈 없음 혹은 이용자 없음
 *              |message        |string         |실패 사유
 *              |data           |json           |
 *              ||cost          |int            |부활에 사용된 비용
 *              ||count         |int            |누적 부활 횟수
 * desc:        게임 중 부활 기능을 사용하고 데이터를 갱신
 *              common 데이터는 18 번을 사용하며, 현재 형태는 이맇게 됨 ["20","40","80","160"]
 *              반환되는 count는 이번 부활을 성공한 결과를 포함
 */
```

### 리더 보드 정보를 획득

```fold
/* desc:	리더 보드 정보를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_game_ranks_pang
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|is_season	|int		|0: 비시즌, 1: 시즌
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 시즌 없음, 3: 실패 - select_01, 4: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|50위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|string		|1: 유아체, 2: 성체
 * desc:	내 이용자 고유값과 시즌 여부를 통해 해당하는 리더 보드를 호출
 *		리더보드는 나의 최고 기록을 포함하지만 정보가 없다면 각각 빈 배열로 반환될 것
 */
```

### 이번 시즌에서 달성한 입장(?) 정보 가져오기

```fold
/* desc:        이번 시즌에서 달성한 입장(?) 정보 가져오기
 * method:      post
 * url:         <http://$>{host}:52532/get_season_rank_pang
 *              |name           |type           |desc
 * input:       |uid_u          |string         |이용자의 고유값
 * output:      |code           |int            |0: 성공 혹은 개인 랭킹 없음, 1: 실패 - select_00, 2: 실패 - 현재 시즌 없음, 3: 실패 - select_01, 4: 실패 - 랭킹 정보 없음, 5: 실패 - select_02
 *              |message        |string         |실패 사유
 *              |data           |array_json     |
 *              ||ranking       |int            |이번 시즌 순위
 *              ||uid_u         |string         |이용자의 고유값
 *              ||nickname      |string         |이용자의 닉네임
 *              ||percent       |float          |이번 시즌 순위 백분율
 *              ||reward        |int            |현재 순위 기준 보상
 *              ||rewards       |array_json     |현재 시즌 보상 목록
 *              |||percent      |int            |상위 X 퍼센트
 *              |||reward       |int            |대응되는 보상의 개수
 *              ||begin_at      |string         |시작 일시
 *              ||end_at        |string         |종료 일시
 *              ||name          |string         |시즌 이름, 숫자일 수도 있고 문자일 수도 있고
 * desc:        이번 시즌에서, 현재 시점으로, 받을 수 있는 보상 등을 반환
 */
```

---

### 모든 세션을 제거

```fold
/* desc:	모든 세션을 제거
 * method:	post
 * url:		<http://$>{host}:52532/del_sessions
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 * output:	|code		|int		|0: 성공
 *		|message	|string		|실패 사유
 *		|data		|json		|뭐 없음
 * desc:	캐터리에 입장할 때 앞서 생성된 모든 세션을 제거함
 *		이미 접속해 있는 기기라면 중간 체크를 할 때 세션 에러로 튕김
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>푸시 알림</span>

### 푸시용 토큰 저장 및 갱신

```fold
/* desc:	푸시용 토큰 저장 및 갱신
 * method:	post
 * url:		<http://$>{host}:52541/set_push_token
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|token		|string		|푸시용 기기 토큰값
 *		|country	|string		|로컬라이징 언어 (KR, JP, US)
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - update_00 or insert_00 failed
 *		|message	|string		|실패 사유
 *		|data		|json		|뭐 없음
 * desc:	푸시를 전송하기 위한 토큰값을 데이터베이스에 저장
 *		로그인이 완료되고 캐터리 입장하는 시점에 호출하여 푸시용 토큰을 전송
 *		- 토큰 값은 앱을 다시 설치할 때 다른 값으로 변경되기 때문
 *		- 설정창에서 언어를 변경할 때마다 호출함이 옳으나, 서버 통신중 로딩 필수가 되므로 일단 배제
 *		동일한 시점에 현재 게임이 사용하고 있는 언어도 같이 전송
 *		푸시 메세지를 위한 on/off 옵션을 만들어야할 것
 */
```

### 개인간 푸시 알림이 필요할 때 호출하는 함수

```fold
/* desc:	개인간 푸시 알림이 필요할 때 호출하는 함수
 * method:	post
 * url:		<http://$>{host}:52541/set_push_p2p
 *		|name		|type		|desc
 * input:	|uid_u_tx	|string		|메세지를 보내는 사람의 고유값
 *		|uid_u_rx	|string		|메세지를 받는 사람의 고유값
 *		|type		|int		|메세지의 타입 (0: 친구 신청, 1: 친구 수락, 2: 선물 전송, 3: 선물 받음)
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - select_01, 3: 그런 타입 없음, 4: 푸시 실패
 *		|message	|string		|실패 사유
 *		|data		|json		|뭐 없음
 * desc:	데이터베이스에 저장된 이용자들의 토큰을 이용해 푸시를 전송
 *		푸시 메세지의 언어는 이전에 저장된 각 이용자의 언어에 맞게 전송
 *		푸시 메세지 전송을 위한 토큰값이 저장되어 있지 않다면 그저 에러를 뱉음
 */
```

---

## ----------------------------------------------

## <span style='color:#8854d0'>슈팅 게임 관련</span>

### 시즌 스테이지를 시작하고 스테이지 정보 가져오기

```fold
/* desc:	[슈팅게임] 시즌 스테이지를 시작하고 스테이지 정보 가져오기
 * method:	post
 * url:		<http://$>{host}:52542/set_season_begin
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 시즌 시드값 없음, 3: 실패 - select_01, 4: 실패 - 그런 캐릭터 없음
, 5: 실패 - insert_00, 6: 실패 - 세션 이미 존재
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||stage		|array string   |스테이지를 구성하는 숫자(문자열)의 배열
 *		||seed		|int		|스테이지를 생성하는데 사용된 seed 값
 *		||uid_s		|int		|시즌의 고유값
 *		||uid_g		|int		|게임의 고유값
 *		||uid_u		|int		|이용자의 고유값
 *		||uid_c		|int		|캐릭터의 고유값
 * desc:	고양이의 정보를 받아 새로운 게임을 생성
 *		시즌 게임에 대한 시작만을 담당
 *		현재 시즌에 따라 총 1024 개의 스테이지 배열을 반환
 *		3월 이후부터 시드값이 바뀔 예정이므로 스테이지 구성이 변경될 것
 */
```

### 스테이지를 진행하고 있는 중간중간 진행 정보 저장하기

```fold
/* desc:	[슈팅게임] 스테이지를 진행하고 있는 중간중간 진행 정보 저장하기
 * method:	post
 * url:		<http://$>{host}:52542/set_game_mid
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 * desc:	스테이지 진행 중간마다 플레이 기록을 저장하고 게임의 정상 진행 여부를 반환
 *		현재 거리 1000, 골드 1000, 캐시 100 이상 차이날 때, 및 각각 차이가 0일 때 오류(3) 반환
 */
```

### 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기

```fold
/* desc:	[슈팅게임] 러닝 게임이 종료되었음을 알리고 게임 및 계정 정보 등을 가져오기
 * method:	post
 * url:		<http://$>{host}:52542/set_game_end
 *		|name		|type		|desc
 * input:       |uid_g		|string		|게임의 고유값
 *		|gold		|int		|현재까지 획득한 전체 골드
 *		|cash		|int		|현재까지 획득한 전체 캐시
 *		|dist		|int		|현재까지 진행한 전체 거리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 비정상 플레이, 4: 실패 - update_00, 5: 실패 - select_03, 6: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||get_exp	|int		|경험치
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname     |string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|10위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||now		|json		|이번 게임 기록
 *		|||is_season	|int		|0: 비시즌, 1: 시즌
 *		|||dist		|int		|도달 거리
 *		|||gold		|int		|획득 골드
 *		|||cash		|int		|획득 캐시
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||name		|string		|캐릭터의 닉네임
 * desc:	게임을 종료하고 필요한 값을 반환
 *		rank 는 내가 달성했던 기록중 가장 랭킹이 높은 게임 기록
 *		ranking 은 서버상 존재하는 가장 랭킹이 높은 10개의 게임 기록 배열
 *		now 는 이번 게임에서 달성한 기록
 */
```

### 슈팅게임 게임에서의 탈주(시즌, 비시즌 공용)

```fold
/* desc:	[슈팅게임] 게임에서의 탈주(시즌, 비시즌 공용)
 * method:	post
 * url:		<http://$>{host}:52542/set_game_escape
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - 세션 없음
 *		|message	|string		|실패 사유
 *		|data		|-		|-
 * desc:	달리기 게임 도중 일시정지를 누르고 탈주할 때 등에 사용
 *		정상 탈주 여부는 code를 통해 확인하며 0일 때만 동작한다고 보면 됨
 *		하지만 어차피 탈주가 목적인데다 세션이 2분 지속되므로 실패해도 에러 메세지를 띄우고 탈주하면 될 듯
 */
```

### 슈팅 게임 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감

```fold
/* desc:	[슈팅 게임] 게임 중 부활 기능을 사용하고 필요한 경우 캐시를 차감
 * method:	post
 * url:		<http://$>{host}:52542/set_resurrect
 *		|name		|type		|desc
 * input:	|is_adv		|int		|광고 부활 여부
 *		|uid_g		|string		|게임의 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 게임 없음, 3: 실패 - select_01, 4: 실패 - 공용 데이터 없음
, 5: 실패 - update_00, 6: 실패 - update_01, 7: 실패 - 더 이상 부활 불가, 8: 실패 - 돈 없음 혹은 이용자 없음
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||cost		|int		|부활에 사용된 비용
 *		||count		|int		|누적 부활 횟수
 * desc:	게임 중 부활 기능을 사용하고 데이터를 갱신
 *		common 데이터는 18 번을 사용하며, 현재 형태는 이맇게 됨 ["20","40","80","160"]
 *		반환되는 count는 이번 부활을 성공한 결과를 포함
 */
```

### 슈팅 게임 리더 보드 정보를 획득

```fold
/* desc:	[슈팅 게임] 리더 보드 정보를 획득
 * method:	post
 * url:		<http://$>{host}:52532/get_game_ranks_shot
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자의 고유값
 *		|is_season	|int		|0: 비시즌, 1: 시즌
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 시즌 없음, 3: 실패 - select_01, 4: 실패 - select_02
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||rank		|json		|내 랭킹 정보
 *		|||ranking	|int		|내 랭킹
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|string		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|int		|도달 거리
 *		|||status	|int		|1: 유아체, 2: 성체
 *		||ranks		|array json	|50위까지의 랭킹 정보
 *		|||ranking	|int		|순위
 *		|||uid_u	|string		|이용자의 고유값
 *		|||uid_c	|string		|캐릭터의 고유값
 *		|||nickname	|string		|이용자의 닉네임
 *		|||level	|int		|이용자의 레벨
 *		|||name		|string		|캐릭터의 닉네임
 *		|||max_dist	|string		|도달 거리
 *		|||status	|string		|1: 유아체, 2: 성체
 * desc:	내 이용자 고유값과 시즌 여부를 통해 해당하는 리더 보드를 호출
 *		리더보드는 나의 최고 기록을 포함하지만 정보가 없다면 각각 빈 배열로 반환될 것
 */
```

### 슈팅 게임 이번 시즌에서 달성한 입장(?) 정보 가져오기

```fold
/* desc:        이번 시즌에서 달성한 입장(?) 정보 가져오기
 * method:      post
 * url:         <http://$>{host}:52532/get_season_rank_shot
 *              |name           |type           |desc
 * input:       |uid_u          |string         |이용자의 고유값
 * output:      |code           |int            |0: 성공 혹은 개인 랭킹 없음, 1: 실패 - select_00, 2: 실패 - 현재 시즌 없음, 3: 실패 - select_01, 4: 실패 - 랭킹 정보 없음, 5: 실패 - select_02
 *              |message        |string         |실패 사유
 *              |data           |array_json     |
 *              ||ranking       |int            |이번 시즌 순위
 *              ||uid_u         |string         |이용자의 고유값
 *              ||nickname      |string         |이용자의 닉네임
 *              ||percent       |float          |이번 시즌 순위 백분율
 *              ||reward        |int            |현재 순위 기준 보상
 *              ||rewards       |array_json     |현재 시즌 보상 목록
 *              |||percent      |int            |상위 X 퍼센트
 *              |||reward       |int            |대응되는 보상의 개수
 *              ||begin_at      |string         |시작 일시
 *              ||end_at        |string         |종료 일시
 *              ||name          |string         |시즌 이름, 숫자일 수도 있고 문자일 수도 있고
 * desc:        이번 시즌에서, 현재 시점으로, 받을 수 있는 보상 등을 반환
 */
```



## ----------------------------------------------

## <span style='color:#8854d0'>미니 게임 공통</span>

### 이번 게임에서 얻은 경험치 호출
```fold
/* desc:	이번 게임에서 얻은 경험치 호출
 * method:	post
 * url:		http://${host}:{52534(run),52537(jump),52540(pang),52542(shot)}/set_exp_v3
 *		|name		|type		|desc
 * input:	|uid_g		|string		|이용자 고유값
 * 		|dist		|int		|획득한 점수
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 세션 없음, 3: 실패 - update_00, 4: 실패 - select_01
 * 		|data		|json		|
 * 		||level		|int		|레벨(레벨업시 지금 레벨과 다를 수 있음)
 *		||exp		|int		|누적된 경험치
 *		||point		|int		|잔여 스킬 포인트
 * desc:	이번 기록을 통해 경험치를 얼마나 획득하는지 계산하고 반환 받음
 *		최근 28일(2시즌)간 달성된 모든 기록들 중 유요한 것들만 추리고, 평균값을 계산에 이용
 *		평균값을 기준으로 20의 경험치 획득, 이외 10% 단위마다 1씩 증감되며 최대치는 40
 */
```

## -------------------------------------------
## <span style='color:#8854d0'>스킨 관련 → 포트 52543</span> 

### 상점에서 스킨 아이템 목록을 가져오기
```fold
/* desc:	상점에서 스킨 아이템 목록을 가져오기
 * method:	post
 * url:		http://${host}:52543/get_skin_packs
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|array json	|
 *		||index		|int		|판매 품목의 고유 번호
 *		||style		|int		|스킨 꾸러미의 번호(재판매 등도 가능하므로 중복될 수 있음)
 *		||part		|string		|2진수 비트 정수
 *		||count		|int		|한정 판매 스킨 판매량/상시 및 코인 전용은 -1
 *		||supply	|int		|한정 판매 스킨 공급량/상시 및 코인 전용은 -1
 *		||price		|int		|이 스킨 꾸러미를 사기 위해 필요한 젤리의 양
 *		||type		|int		|0: 한정, 1: 상시, 2: 코인/무료
 *		||is_active	|int		|활성화 여부(0: 판매 중지, 1: 판매 중, 2: 테스트)
 * desc:	현재 판매중인 스킨의 상점 정보들을 반환
 *		각 스킨이 가지는 고유한 정보들도 포함되므로 주의 필요
 *		같은 이유로 상점에서 보여지지 않더라도 해당 아이템들은 디비상에서 삭제 금지
 *		동일 style에서도 파트별 차이를 둘 가능성이 높기에 스타일과 파트는 분리
 *		type이 0이라면 상점에 띠지 및 남은 개수를 보여주면 됨
 */
```

### 내 스킨 목록 가져오기
주의: 스킨이 없을때도 성공 케이스
```fold
/* desc:	내 스킨 목록 가져오기
 * method:	post
 * url:		http://${host}:52543/get_skins_my
 *		|name		|type		|desc
 * input:       |uid_u		|string		|이용자 고유값
 * output:      |code		|int		|0: 성공(스킨 없음 포함), 1: 실패 - select_00
 *		|message|string |실패 사유
 *		|data		|		|
 *		||index		|int		|판매 품목의 고유 번호
 *		||uid_c		|string		|캐릭터 고유값(미착용시 null 반환)
 *		||style		|int		|스킨의 스타일, 분홍 한복 파트인지, 파란 한복 파트인지
 *		||part		|int		|비트로 구성됨, (등, 몸, 얼굴, 머리, 꼬리) 만약 10이라면 몸과 머리만 포함됨
 *		||type		|int		|스킨의 희귀도(0: 한정, 1: 상시젤리, 2: 상시코인)
 * desc:내가 가지고 있는 모든 스킨을 반환
 */
```

### 내 파트별 스킨 목록 가져오기
```fold
/* desc:	내 파트별 스킨 목록 가져오기
 * method:	post
 * url:		http://${host}:52543/get_part_skins_my
 *		|name		|type		|desc
 * input:	
 *      |uid_u		|string		|이용자 고유값
 * 		|part		|int		|비트로 구성됨, (등, 몸, 얼굴, 머리, 꼬리) 만약 10이라면 몸과 머리만 포함됨
 * 		|is_equip	|int		|0: 착용 여부 관계 없이 모두, 1: 착용 상태인 것만, 2: 미착용 상태인 것만
 * output:	|code		|int		|0: 성공(스킨 없음 포함), 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|		|
 *		||index		|int		|스킨 파트의 인벤토리상 고유번호
 *		||uid_c		|string		|캐릭터 고유값(미착용시 null 반환)
 *		||style		|int		|스킨의 스타일, 분홍 한복 파트인지, 파란 한복 파트인지
 *		||part		|int		|비트로 구성됨, (등, 몸, 얼굴, 머리, 꼬리) 만약 10이라면 몸과 머리만 포함됨
 * desc:	파트별로 내가 가지고 있는 스킨들을 표시해줌
 * 		조건에 따라 착용 여부에 대한 반환값이 달라지므로 참고
 */
```

### 캐릭터가 착용 중인 스킨 가져오기
```fold
/* desc:	캐릭터가 착용 중인 스킨 가져오기
 * method:	post
 * url:		http://${host}:52543/get_skins_cat
 *		|name		|type		|desc
 * input:	|uid_c		|string		|캐릭터 고유값
 * output:	|code		|int		|0: 성공(스킨 없음 포함), 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|array_json	|
 *		||index		|int		|스킨 파트의 고유번호
 *		||style		|int		|스킨의 스타일, 분홍 한복 파트인지, 파란 한복 파트인지
 *		||part		|int		|비트로 구성됨, (등, 몸, 얼굴, 머리, 꼬리) 만약 10이라면 몸과 머리만 포함됨
 * desc:	index는 아이템으로써의 고유값
 * 		style은 해당 아이템이 어떤 종류의 스킨인지를 알려주고 part는 그 중에서도 어떤 부위인지를 알려줌
 */
```

### 캐릭터에 대한 스킨을 탈착하기
```fold
/* desc:	캐릭터에 대한 스킨을 탈착하기
 * method:	post
 * url:		http://${host}:52543/toggle_skin_equip
 *		|name		|type		|desc
 * input:	|uid_c		|string/int	|캐릭터 고유값(장비 해제를 원한다면 -1)
 * 		|skin_index	|int		|스킨 파트의 인벤토리상 고유번호
 * output:	|code		|int		|0: 성공(스킨 없음 포함), 1: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|		|뭐 없음
 * desc:	캐릭터에 대한 스킨 착용을 바란다면 uid_c 는 캐릭터의 고유값
 * 		캐릭터에 대한 스킨 해제를 바란다면 uid_c 는 -1
 * 		skin_index 는 다른 기능에서의 index와 동일한 의미로 동작
 */
```

### 상점으로부터 스킨 꾸러미 구매
```fold
/* desc:	상점으로부터 스킨 꾸러미 구매
 * method:	post
 * url:		http://${host}:52543/buy_skin_pack
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 *		|shop_index	|int		|상점 스킨 꾸러미 고유번호
 * output:	|code		|int		|0: 성공(스킨 없음 포함), 1: 실패 - select_00, 2: 실패 - select_01 혹은 돈 없음, 3: 실패 - insert_00, 4: >실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|뭐 없음
 *		||cash		|int		|남은 캐시
 *		||gold		|int		|남은 코인
 *		||arr_bought	|array json	|
 *		|||style	|int		|스킨의 스타일, 분홍 한복 파트인지, 파란 한복 파트인지
 *		|||part		|int		|비트로 구성됨, (등, 몸, 얼굴, 머리, 꼬리)
 * desc:	한정판 스킨을 구매하고 남은 상품 수 및 이용자의 캐시를 차감
 *		획득한 스킨은 arr_bought의 style 및 part를 통해 구분 가능
 */
```
## -------------------------------------------
## <span style='color:#8854d0'>챗봇 → 서버 주소 유의</span>
### 일상대화용 고양이 챗봇
```
/* desc:	일상대화용 고양이 챗봇
 * method:	post
 * url:		http://3.35.218.21:52532/nyangbot
 *		|name		|type		|desc
 * input:	|chat		|string		|입력된 대화문
 * 		|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패
 *		|data		|		|
 *		||msg		|string		|답변 대화문
 *		||count_max	|int		|최대 대화 횟수
 *		||count_remain	|int		|잔여 대화 횟수
 * desc:	이용자의 대화를 입력받아 적절한 답변을 생성 및 반환
 * 		chat 에 내용을 담지 않거나, 설령 chat을 보내지 않더라도 답변은 주어짐
 * 		이때, '때로 말하지 않으면 모르는 법이다냥' 문장을 반환
 */
```

### 대화 횟수 획득
```
/* desc:	대화 횟수 획득
 * method:	post
 * url:		http://3.35.218.21:52532/get_count
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공
 * 		|data		|		|
 *		||count_max	|int		|최대 대화 횟수
 *		||count_remain	|int		|잔여 대화 횟수
 * desc:	이용자의 잔여 대화 수 및 최대 대화 횟수를 반환
 * 		광고를 보지 않아도 매일 오전 9시에 횟수 초기화
 */
```

### 광고 시청 완료(냥봇)
```
/* desc:	광고 시청 완료
 * method:	post
 * url:		http://3.35.218.21:52532/set_ad
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - 대화 기록 없음, 2: 실패 - 대화 횟수 남아 있음
 * 		|data		|		|
 *		||count_max	|int		|최대 대화 횟수
 *		||count_remain	|int		|잔여 대화 횟수
 * desc:	광고를 모두 시청했을 경우 채팅 횟수를 리필
 * 		지금은 최대 횟수에서 40% 를 더 추가해줌
 */
```
## -------------------------------------------
## <span style='color:#8854d0'>랭킹</span>
### 이번 시즌 랭킹 정보 호출 
↳ 기존 로비 랭킹 호출의 **대체API** (2023-10-18)
```fold
/* desc:        이번 시즌 랭킹 정보 호출
 * method:      post
 * url:         http://${host}:{52534(run),52537(jump),52540(pang),52542(shot)}/get_season_rank
 *              |name           |type           |desc
 * input:       |uid_u          |string         |내 이용자 고유값
 * output:      |code           |int            |0: 성공, 1: 실패 - select_00, 2: 실패 - select_01
 *              |data           |               |
 *              |-rank_my       |json           |내 랭킹 정보
 *              |--ranking      |int            |내 랭킹(없으면 0)
 *              |--uid_c        |string         |내 캐릭터 고유값(없으면 "")
 *              |--nickname     |string         |내 닉네임(없으면 "")
 *              |--percent      |float          |내 순위 백분율(없으면 "100")
 *              |--reward       |string         |내 보상 개수(없으면 0)
 *		        |--level	    |int		    |내 계정 레벨(없으면 0)
 *		        |--dist		    |int		    |내 최고 기록(없으면 0)
 *		        |--status	    |int		    |내 캐릭터 상태(0: 없을 때, 1: 코네코, 2: 코이네코)
 *              |--skin         |array json     |캐릭터 스킨 정보(없으면 [])
 *              |---style       |int            |스킨 종류
 *              |---part        |int            |스킨 부위
 *              |---type        |int            |스킨 등급
 *              |-ranks         |array json     |시즌 랭킹 정보
 *              |--ranking      |int            |이용자 랭킹
 *              |--uid_c        |string         |캐릭터 고유값
 *              |--uid_u        |string         |이용자 고유값
 *              |--nickname     |string         |이용자 닉네임
 *              |--level        |int            |이용자 레벨
 *              |--status       |int            |이용자의 캐릭터 상태(1: 코네코, 2: 코이네코)
 *              |--max_dist     |int            |최대 도달 거리
 *              |--skin         |array json     |캐릭터 스킨 정보(없으면 [])
 *              |---style       |int            |스킨 종류
 *              |---part        |int            |스킨 부위
 *              |---type        |int            |스킨 등급
 *              |-season        |array json     |이번 시즌 정보
 *              |--begin_at     |string         |시즌 시작 시점
 *              |--end_at       |string         |시즌 종료 시점
 *              |--name         |string         |시즌 이름
 *              |--rewards      |array json     |시즌 보상 배열
 *              |---percent     |string         |해당하는 백분율
 *              |---reward      |string         |백분율 달성시 획득 보상 개수
 * desc:        로비에서 랭킹을 불러오는데 사용
 *              rank_my 는 이번 시즌 중 나의 기록을 담고 있음
 *              ranks 는 이번 시즌 중 이용자 전체의 기록을 담고 있음
 *              season 은 이번 시즌 정보를 담고 있음
 */
```

### 이번 게임 종료 및 랭킹 정보 호출
↳ 기존 게임 종료 및 랭킹 받아오기의 **대체 API** (2023-10-19)
```fold
/* desc:	이번 게임 종료 및 랭킹 정보 호출
 * method:	post
 * url:		http://${host}:{52534(run),52537(jump),52540(pang),52542(shot)}/set_game_end_v2
 *		|name		|type		|desc
 * input:	|uid_g		|string		|게임의 고유값
 * 		|dist		|int		|획득한 점수
 * 		|gold		|int		|획득한 코인
 * 		|cash		|int		|획득한 젤리
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 세션 없음, 3: 실패 - update_00, 4: 실패 - select_01
 * 		|data		|		|
 * 		|-get_exp	|int		|획득한 경험치(항상 10)
 *		|-rank_my	|json		|내 랭킹 정보
 *		|--ranking	|int		|내 랭킹(없으면 0)
 *		|--uid_c	|string		|내 캐릭터 고유값(없으면 "")
 *		|--nickname	|string		|내 닉네임(없으면 "")
 *		|--level	|int		|내 계정 레벨(없으면 0)
 *		|--dist		|int		|내 최고 기록(없으면 0)
 *		|--status	|int		|내 캐릭터 상태(0: 없을 때, 1: 코네코, 2: 코이네코)
 *		|--skin		|array json	|캐릭터 스킨 정보(없으면 [])
 *		|---style	|int		|스킨 종류
 *		|---part	|int		|스킨 부위
 *		|---type	|int		|스킨 등급
 *		|-ranks		|array json	|시즌 랭킹 정보
 *		|--ranking	|int		|이용자 랭킹
 *		|--uid_c	|string		|캐릭터 고유값
 *		|--uid_u	|string		|이용자 고유값
 *		|--nickname	|string		|이용자 닉네임
 *		|--level	|int		|이용자 레벨
 *		|--status	|int		|이용자의 키랙터 상태(1: 코네코, 2: 코이네코)
 *		|--max_dist	|int		|최대 도달 거리
 *		|--skin		|array json	|캐릭터 스킨 정보(없으면 [])
 *		|---style	|int		|스킨 종류
 *		|---part	|int		|스킨 부위
 *		|---type	|int		|스킨 등급
 *		|-now		|json		|이번 게임 기록
 *		|--dist		|int		|도달 거리
 *		|--gold		|int		|획득 코인
 *		|--cash		|int		|획득 젤리
 *		|--uid_c	|string		|캐릭터의 고유값
 *		|--name		|string		|캐릭터의 닉네임
 * desc:	게임 종료 후 랭킹을 불러오는데 사용
 * 		rank_my 는 이번 시즌 중 나의 기록을 담고 있음
 * 		ranks 는 이번 시즌 중 이용자 전체의 기록을 담고 있음
 * 		now 는 이번 게임에서 달성한 기록을 담고 있음
 */
```


## -------------------------------------------
## <span style='color:#8854d0'>하우징(방꾸미기)</span>

### 이용자가 가진 모든 hex를 호출
```fold
/* desc:	이용자가 가진 모든 hex를 호출
 * method:	post
 * url:		http://${host}:52544/get_hexes
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - 그런 이용자 없음, 3: >실패 - insert_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid		|string		|그리드 고유값
 *		||uid_u		|string		|이용자 고유값
 *		||pos_x		|int		|x 좌표
 *		||pos_y		|int		|y 좌표
 *		||wall		|int		|벽지 종류
 *		||floor		|int		|바닥 종류
 * desc:	이용자가 보유하고 있는 모든 hex grid 를 호출
 *		각 hex 그리드는 wall, floor 와 같이 벽지 및 바닥재 종류를 포함
 *		만약 hex 를 단 1 칸도 가지지 않은 유효한 이용자라면 (0,0) 좌표 한 칸을 만들어 줌
 */
```

### 단일 hex 호출
이건 이용자가 가진 육각 그리드 중 선택된 것만 호출하고 근처에 개방 가능한 그리드도 같이 호출
```fold
/* desc:	단일 hex 호출
 * method:	post
 * url:		http://${host}:52544/get_hex
 *		|name		|type		|desc
 * input:	|uid_h		|string		|그리드 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - select_01
 *		|message	|string		|실패 사유
 *		|data		|json array	|
 *		||x		|int		|그리드 x 좌표
 *		||y		|int		|그리드 y 좌표
 *		||is_open	|int		|좌표 확장 여부
 * desc:	단일 그리드의 정보를 획득
 *		이때, 해당 그리드에 인접한 그리드 개방 여부를 함께 반환
 */
```

### 상점에 존재하는 브랜드 및 모든 가구 호출
```fold
/* desc:	상점에 존재하는 브랜드 및 모든 가구 호출
 * method:	post
 * url:		http://${host}:52544/get_shop_furns
 *		|name		|type		|desc
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid		|string		|가구의 고유값
 *		||brand		|json array	|브랜드
 *		|||index	|int		|상점의 brand과 매칭
 *		|||name		|string		|브랜드 이름
 *		||shop		|json array	|상점 리스트
 *		|||brand	|int		|브랜드 index와 매칭
 *		|||name		|string		|브랜드 이름
 *		|||type		|int		|가구 종류, 각 가구 이미지와 매칭
 *		|||price	|int		|가격
 *		|||price_type	|int		|0: 코인, 1: 젤리
 *		|||size_x	|int		|x축 길이
 *		|||size_y	|int		|y축 길이
 *		|||is_wall	|int		|0: 바닥 가구, 1: 벽 가구
 * desc:	브랜드 정보와 가구 정보를 모두 불러옴
 *		이때, 브랜드 정보의 index는 가구 정보의 brand과 동일함
 *		이후 배치된 가구의 size_x 및 size_y는 회전 값에 따라 서로 반전시키면 됨
 */
```

### 이용자가 보유한 가구 리스트를 호출
```fold
/* desc:	이용자가 보유한 가구 리스트를 호출
 * method:	post
 * url:		http://${host}:52544/get_furns
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00
 *		|message	|string		|실패 사유
 *		|data		|json array	|
 *		||uid		|string		|가구의 고유값
 *		||uid_h		|string		|방(hex)의 고유값
 *		||brand		|int		|브랜드 index
 *		||type		|int		|가구의 종류
 *		||wall		|int		|0: 바닥, 1: 왼쪽 벽, 2: 오른쪽 벽
 *		||pos_x		|int		|x축에서의 좌표
 *		||pos_y		|int		|y축에서의 좌표
 *		||rot		|int		|가구의 회전값, 0: 기본, 1: 회전됨
 *		||price		|int		|가구를 살 당시의 가격
 *		||price_type	|int		|재화 타입, 0: 코인, 1: 젤리
 * desc:	이용자가 구매해서 배치해 놓은 가구 전체를 반환
 *		이미 배치했다고 가정할 때, 가구 사이즈가 필요한지는 아직 모르겠음
 *		판매시 가격은 이벤트로 싸게 풀린 가구를 되팔이해 인플레이션이 유발됨을 방지
 */
```

### 상점에서 가구를 구매 처리하고 구매된 가구 정보 호출
에러코드:
`3 → 캐시 부족`
`4 → 골드 부족`
```fold
/* desc:	상점에서 가구를 구매 처리하고 구매된 가구 정보 호출
 * method:	post
 * url:		http://${host}:52544/set_furn_buy
 *		|name		|type		|desc
 * input:	|uid_u		|string		|이용자 고유값
 *		|uid_h		|string		|방(hex) 고유값
 *		|uid_f		|string		|가구(상점에서의) 고유값
 *		|wall		|int		|0: 바닥, 1: 왼쪽 벽, 2: 오른쪽 벽
 *		|pos_x		|int		|x축에서의 좌표
 *		|pos_y		|int		|y축에서의 좌표
 *		|rot		|int		|가구의 회전값, 0: 기본, 1: 회전됨
 * output:	|code		|int		|0: 성공, 1: 실패 - 이용자, 집, 가구 중 뭐가 없음, 2: 실패 - insert_00
 *		|message	|string		|실패 사유
 *		|data		|json array	|
 *		||uid		|string		|가구의 고유값
 *		||uid_h		|string		|방(hex)의 고유값
 *		||brand		|string		|브랜드 index
 *		||type		|int		|가구의 종류
 *		||wall		|int		|0: 바닥, 1: 왼쪽 벽, 2: 오른쪽 벽
 *		||pos_x		|int		|x축에서의 좌표
 *		||pos_y		|int		|y축에서의 좌표
 *		||rot		|int		|가구의 회전값, 0: 기본, 1: 회전됨
 *		||price		|int		|가구를 살 당시의 가격
 *		||price_type	|int		|재화 타입, 0: 코인, 1: 젤리
 * desc:	이용자가 구매해서 배치해 놓은 가구 전체를 반환
 *		이미 배치했다고 가정할 때, 가구 사이즈가 필요한지는 아직 모르겠음
 *		판매시 가격은 이벤트로 싸게 풀린 가구를 되팔이해 인플레이션이 유발됨을 방지
 */
```

### 가구 이동
```fold
/* desc:	가구 이동
 * method:	post
 * url:		http://${host}:52544/set_furn_move
 *		|name		|type		|desc
 * input:	|uid_f		|string		|가구 고유값
 *		|pos_x		|int		|x 좌표
 *		|pos_y		|int		|y 좌표
 *		|rot		|int		|회전값, 0 혹은 1
 * output:	|code		|int		|0: 성공, 1: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_f		|string		|가구 고유값
 *		||pos_x		|int		|변경된 x 좌표
 *		||pos_y		|int		|변경된 y 좌표
 *		||rot		|int		|회전값, 0 혹은 1
 * desc:	가구의 위치나 회전값을 변경하고 해당하는 결과를 반환
 */
```

### 선택한 가구를 판매하고 환불 받음
```fold
/* desc:	선택한 가구를 판매하고 환불 받음
 * method:	post
 * url:		http://${host}:52544/set_furn_sell
 *		|name		|type		|desc
 * input:	|uid_f		|string		|가구 고유값
 * output:	|code		|int		|0: 성공, 1: 실패 - select_00, 2: 실패 - update_00
 *		|message	|string		|실패 사유
 *		|data		|json		|
 *		||uid_f		|string		|가구 고유값
 *		||uid_u		|string		|이용자 고유값
 *		||price_type	|int		|0: 코인, 1: 젤리
 *		||refund	|int		|환불된 금액
 * desc:	가구를 판매하고 돈을 돌려 받음
 *		이때 돌려 받는 금액은 원가의 80%
 */
```

### 비용을 내고 방(hex) 확장
```fold
{request /set_hex
{
	uid_u: string	/이용자의 고유값
	pos_x: int		/x 좌표
	pos_y: int		/y 좌표
}

response
{
	code: int		/0: 성공, 1~: 실패
	message:	string	/실패사유
	data: {
		uid: string	/그리드 고유값
		uid_u: string	/이용자 고유값
		pos_x: int		/x 좌표
		pos_y: int		/y 좌표
		gold: int		/보유한 골드
	}
}

방 확장 에러 코드
code, message
1, select_00 failed
1, insert_01 failed
2, already bought
3., not enough gold
```
## -------------------------------------------
