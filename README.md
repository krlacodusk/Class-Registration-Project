# 💻Class-Registration-Project
Database Programming Project

📒 프로젝트명

	올클각
	
	
📒 사용기술

	#JAVA #HTML #CSS #JAVASCRIPT #JSP #MVC #ORACLE #CONNECTION POOL


📒 개요

	수강신청 할 때 모두들 서버시간 보여주는 페이지와 교내 수강신청 사이트를 함께 틀어놓고 시작한다.
	이렇듯 매학기마다 전교생이 들어가는 사이트이지만 학생들의 편의를 위한 기능이 추가되지 않고 있다.
	학생들이 좀 더 편리하게 수강신청 사이트를 이용하게 하기 위해 올클각이라는 프로젝트를 진행하게 되었다.

	기존 교내 수강신청 사이트의 기능들을 그대로 유지하고
	  + 서버 시간을 보여주는 기능
	  + 빈시간 강의추천 기능
	  + 위시리스트에 해당 강의를 몇 명의 학생들이 담았는지 보여주는 기능
	  등 추가하였다.


📒 데모영상
+ 학생용 수강신청
 
	https://drive.google.com/file/d/1q2jfnPUnMLRDtrwZQ-ZuaJgeSusVsm7O/view?usp=sharing

+ 교수용 수강신청
 
	https://drive.google.com/file/d/17jDaXhEdpM376VJwhPa5WKIHzc9wSR9y/view?usp=sharing


📒 세부기능

![기능1](https://user-images.githubusercontent.com/57470848/146861298-337ddaeb-195b-4375-a258-3eb5fafac000.png)
![기능2](https://user-images.githubusercontent.com/57470848/146861289-fcc63d5b-4d1c-415f-852a-4087e8afb00c.png)


📒 데이터베이스 설계

![데이터베이스설계](https://user-images.githubusercontent.com/57470848/146862598-8d718038-ede1-4d31-9fd8-d467e885bbaf.png)


📒 USECASE
![usecase](https://user-images.githubusercontent.com/57470848/146862435-2bd424b4-cb6d-420b-8416-7b0e8fd3c7a0.png)


📒 어려웠던 알고리즘
create or replace view recView as
select distinct d.c_id cid, d.class_num cnum, cname, course.prof_id pid, course.credit credit
from course_dinfo d, course "
where course.c_id = d.c_id and course.class_num = d.class_num and 
(d.c_id, d.class_num) not in (select c_id, class_num 	     from course_dinfo d  
where (day_week, times) in (select distinct d.day_week dday_week, d.times dtimes 
from wish w, course_dinfo d 	                                                                             where w.c_id = d.c_id and 
w.class_num = d.class_num and 
w.stu_id = " + stuId + " and w.wish_id = " + wishNum + "))



📒 사용법

+ 학생ver


		login.jsp
			학생 로그인
			id: 20170928
			pw: 121212

		meun.jsp
			* 로그인 후 서버시간, 내 정보가 올바르게 뜨는지 확인
			* top bar로 각각 수강신청, 위시리스트, 내 시간표 메뉴로 이동하는지 확인(단, 수강신청 메뉴는 수강신청 기간인 경우만)
			* 수강 신청 기간이 아닌 경우 수강신청 버튼 위에 '수강신청 기간이 아닙니다.' 안내 메세지 뜨면서 
			  수강신청 버튼, top bar의 수강신청탭 block
			* 수강 신청 기간을 바꾸기 위해 menu.jsp 56번째 줄 h(시간), m(분), s(초)를 바꿔주기(24시간 형식)
			* 수강 신청 기간이 맞는 경우 수강신청 버튼, top bar의 수강신청 탭 활성화

		takes.jsp
			* 학수번호로 강의 검색 하기 위해서 '컴퓨' or '컴퓨K0055' 입력 후 검색
			* 학과명으로 강의 검색 시 '회' or '회화' 입력 후 검색
			* 교수명으로 강의 검색 시 '박창섭' 검색
			* 과목명으로 강의 검색 시 '데' or '데이터베이스프로그래밍' 입력 후 검색
			* 검색 결과로 나오는 과목이 현재수강인원이 최대수강인원을 넘지않고 수강신청 결과에 있는 과목과 시간대가 겹치지않는 경우 
			  신청을 누르면 수강신청 결과 리스트로 추가됨
			* 만약 겹치거나 최대수강신청인원을 초과하는 경우 해당 오류문을 alert로 띄운후 수강신청이 안되도록 함

			* 최종 위시리스트를 이용해 수강신청을 하는 경우 위시리스트 메뉴에서 최종으로 정한 위시리스트가 우선순위 순서로 뜸
			* 만약 위시리스트를 아예 작성하지못한 경우 뜨지않고 위시리스트를 작성했지만 최종 위시리스트를 정하지 못한 경우
			  디폴트로 설정해둔 위시리스트가 뜸
			* 신청을 누를때 해당 과목이 현재수강인원이 최대수강인원을 넘지않고 수강신청 결과에 있는 과목과 시간대가 겹치지않는 경우
			   수강신청 결과 리스트로 추가되고 최종 위시리스트에서는 빠지고 위시리스트 NO값이 자동으로 빠진값의 번호를 채워줌
			* 만약 겹치거나 최대수강신청인원을 초과하는 경우 해당 오류문을 alert로 띄운후 수강신청이 안되도록 함

			* 수강신청 결과는 강의검색, 최종 위시리스트에서 수강 신청한 과목들의 결과를 보여줌 
			* 이때 수강 취소를 하고싶은 강의는 삭제를 클릭하면 삭제됨

			* top bar로 바로 메인으로 나가거나 내 시간표를 확인하거나 로그아웃을 할  수 있음 (위시리스트 메뉴로는 갈 수 없음)

		wish.jsp
			* 학수번호로 강의 검색 하기 위해서 '컴퓨' or '컴퓨K0019' 입력 후 검색
			* 학과명으로 강의 검색 시 '실' or '실음' 입력 후 검색
			* 교수명으로 강의 검색 시 '김병일' 검색
			* 과목명으로 강의 검색 시 '미술' or '미술관교육의이론과실제' 입력 후 검색
			* 검색 결과로 나오는 강의를 위시리스트에 담기 위해서 담기를 클릭 ->
			   이미 담은 강의가 아니면 위시리스트에 추가됨(담은 인원을 초과해도 추가됨)

			* 위시리스트에는 강의 검색, 빈시간 강의추천을 통해 담은 강의 목록을 보여줌
			* 담아있는 강의들에게 우선순위를 줄 수 있고 확인 버튼으로 확정( 우선 순위를 못 정한 과목은 공백으로 둘 수 있음 )
			* 위시리스트에서 빼고싶은 강의는 삭제를 클릭해서 지울 수 있음
			* 위시리스트 추가하기를 누르면 새로운 위시리스트가 뜸(여기에도 위와 같이 강의를 담고 우선순위를 줄 수 있음)
			* 위시리스트를 추가하면 select박스에 추가된 위시리스트 번호가 뜸(이를 통해 다른 위시리스트로 옮겨갈 수 있음)
			* 위시리스트 삭제하기를 누르면 해당하는 위시리스트 자체가 삭제됨
			* 최종 위시 설정을 원하는 위시리스트 번호를 select박스에서 고르고 설정하면 수강신청 메뉴로 넘어갈 위시리스트가 설정됨

			* 위시시간표는 보기 버튼을 클릭하면 위시리스트 담은 과목들의 시간표를 보여줌
			   (시간대가 겹치는 강의는 같이 표시됨(ex, 미술관교육의이론과실제, 음악감상론2(김광민)))

			* 빈시간 강의 추천은 검색 버튼을 누르면 위시리스트에 담은 과목의 시간대를 제외한 강의들의 목록을 보여줌
			* 신청을 누르면 위시리스트에 헤당강의기 들어감

			* top bar로 바로 메인으로 나가거나 내 시간표를 확인하거나 로그아웃을 할  수 있음 (수강신청 메뉴로는 갈 수 없음)

		table.jsp
			* 수강신청 결과인 과목들의 시간표를 볼 수 있음 

			* top bar로 바로 메인으로 나가거나 수강신청 메뉴, 위시리스트 메뉴로 이동, 로그아웃을 할  수 있음

+ 교수ver


		login.jsp
			교수 로그인
			id: 1002
			pw: 1002

		pmenu.jsp
			* 내 정보(아이디, 이름, 학과)가 제대로 뜨는지 확인
			* top bar로 메인, 수강신청, 위시리스트 메뉴로 이동

		ptakes.jsp
			* 해당 교수가 담당하는 과목의 수강신청 결과 수강인원를 알 수 있음 
			* top bar로 바로 메인으로 나가거나 위시리스트 메뉴로 이동, 로그아웃을 할  수 있음
		pwish.jsp
			* 해당 교수가 담당하는 과목에 대해 학생들이 최종 위시리스트로 설정한 위시리스트 기준으로 담은 윈원을 보여줌
			* top bar로 바로 메인으로 나가거나 수강신청 메뉴로 이동, 로그아웃을 할  수 있음
