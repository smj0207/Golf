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


