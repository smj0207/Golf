# 2022.05월 산업기사 문제

## 수강신청페이지이다

![image](https://user-images.githubusercontent.com/97486300/207482536-5abd6805-64e7-4029-a0f9-73c4e3595af3.png)

## chkVal함수

```javaScript
function chkVal() {
		var cls = document.classData;
		
		if(!cls.resist_month.value) {
			alert("수강월이 입력되지 않았습니다!");
			cls.resist_month.focus();
			return false;
	}
```

chkVal에서 유효성검사를 해주며 

![image](https://user-images.githubusercontent.com/97486300/207495876-14a7cc20-a36b-44c8-b3f9-f1fb26014633.png)

값이 입력되지 않았을 경우 메세지가 뜨면서 포커스를 빈칸으로 이동시켜준다

## 회원명

![image](https://user-images.githubusercontent.com/97486300/207483360-0e7fb7f0-e8d1-4844-ba37-f119d4d3fe01.png)

![image](https://user-images.githubusercontent.com/97486300/207483415-3003307f-db2a-4d0f-a566-83565a3bf9c7.png)

회원명을 바꾸게 되었을때 회원번호 또한 회원명에 맞게 자동으로 바뀌게 된다

```
function vDisplay(code) {
		document.classData.c_no.value = code; 	
		document.classData.class_name.value = "none"; 
		document.classData.tuition.value = ""; 	
	}
```

vDisplay에서 매개변수값을 받아와 value값으로 변경해줘 회원번호에 넣어준 후 <br>
강의명은 none으로 수강료는 빈 문자열로 설정시켜준다.

![image](https://user-images.githubusercontent.com/97486300/207486765-101cde0d-8002-4218-b25f-90939c1cefc3.png)

회원번호가 20000을 넘는 경우는 수강료를 50% 할인해준다는 메세지를 출력해준다

```
function calTuition(tcode) {
		var mbr = document.classData.c_no.value;
		if(!mbr) {
			alert("회원명을 먼저 선택하세요.");
			document.classData.class_name[0].selected = true;
			document.classData.c_name.focus();
		} else {
			
			var salePrice = 0;
			switch (tcode) {
				case "100":
					salePrice = 100000;
					break;
				case "200":
					salePrice = 200000;
					break;
				case "300":
					salePrice = 300000;
					break;
				case "400":
					salePrice = 400000;
					break;
			}
			
			if(mbr.charAt(0)=='2') {
				alert("수강료가 50% 할인 되었습니다.");
				salePrice = salePrice / 2;
			}
			
			document.classData.tuition.value = salePrice;
		}
	}
```

회원코드를 불러온 값의 맞는 값을 출력해주며 <br>
if문으로 회원번호의 첫번째가 2인 경우 수강료를 2로 나누어 50% 할인해주는 문구를 출력하게 해준다.

## 수강신청

![image](https://user-images.githubusercontent.com/97486300/208014543-21fb808a-15e1-4dc2-8312-ce52cf2da158.png)

수강 신청을 하게 되면 메인페이지로 돌아가지고

![image](https://user-images.githubusercontent.com/97486300/208014610-7802b9c7-6a2c-4f93-a2eb-43d61d718c37.png)

회원정보조회 페이지에 입력이 된다

## 다음은 강사매출 현황이다

![image](https://user-images.githubusercontent.com/97486300/208014865-d28ee9d4-cd83-4fd2-a745-e1426416aeae.png)

현재는 고급반에 매출이 없다
고급반에 수강신청을 해보겠다

![image](https://user-images.githubusercontent.com/97486300/208014947-4d318251-a264-414c-8fe6-ad2a11396372.png)

정상적으로 고급반에 강사 매출이 오른걸 확인 할 수 있다



![image](https://user-images.githubusercontent.com/97486300/208015053-d25b5138-c1b7-460d-8af3-9c8d2a9fea55.png)

## 회원정보페이지에 코드 설명이다

```
<%
	StringBuffer sb = new StringBuffer();
	sb.append("select substr(c.resist_month,1,4)||'년'||substr(c.resist_month,5,2)||'월' resist_month,");
	sb.append(" c.c_no, m.c_name, t.class_name, c.class_area,");
	sb.append(" '￦'||to_char(c.tuition, '999,999') tuition, m.grade");
	sb.append(" from tbl_class_202201 c, tbl_member_202201 m, tbl_teacher_202201 t");
	sb.append(" where c.c_no = m.c_no and c.teacher_code = t.teacher_code");
%>
```

쿼리문에 데이터를 가공해서 

```
<table>
			<thead>
				<tr>
					<th>수강월</th>
					<th>회원번호</th>
					<th>회원명</th>
					<th>강의명</th>
					<th>강의장소</th>
					<th>수강료</th>
					<th>등급</th>
				</tr>
			</thead>
			<tbody>
				<%
					while(rs.next()) {
				%>
				<tr>
					<td><%= rs.getString(1) %></td>
					<td><%= rs.getString(2) %></td>
					<td><%= rs.getString(3) %></td>
					<td><%= rs.getString(4) %></td>
					<td><%= rs.getString(5) %></td>
					<td><%= rs.getString(6) %></td>
					<td><%= rs.getString(7) %></td>
				</tr>
				<%
					}
				%>
			</tbody>
		</table>
```
테이블에 rs.getString 에서 출력 시켜준다

## 강사매출페이지

또한 회원정보페이지와 거의 유사하지만 sum함수로 강사 매출을 더하여 출력해준다 
```
sb.append("select t.teacher_code, t.class_name, t.teacher_name, '￦'||to_char(sum(c.tuition), '999,999') tuition");
```
