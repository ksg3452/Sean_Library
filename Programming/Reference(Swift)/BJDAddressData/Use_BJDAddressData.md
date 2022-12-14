# How to use **'BJDAddressData'**

 해당 자료는 대한민국 전 영토의 시/군/구 의 정보를 사용하는 앱을 만들다가 작성하게 되었다.
 해당 방식의 자료는 "https://github.com/AssistoLab/DropDown" 의 라이브러리를 사용할 때 특화되게 만들었다.
 
 selectCityNm, selectSggNm, selectEmdNm 변수는 String 형 변수다.
 - Korea 라는 구조체에서 내부 함수인 selectSgg() 와 selectEmd() 을 이용하기 위한 변수로 서 외부에서 해당 Struct 의 저 변수들 중 사용하고자 하는 함수에 맞게 값을 넣는 용도로 사용이 된다.


 cityNm 변수는 String Array 형의 변수이다.
- 해당 변수의 경우에는 전국의 *'광역시/도'* 의 이름이 전부 들어가있다.
- 양이 그렇게 많지 않기에 다른 명령을 사용하지 않고 바로 변수에 넣어 두었다.

selectSgg() 는 인자를 받을 매개 변수는 없지만 String Array 를 반환한다.
- Struct Korea 에 **selectCityNm** 변수가 지정이 되어있지 않을 경우 원하는 값을 받을 수 없다.
- sggNm 은 String Array 형의 변수이다.
    - 해당 함수는 원하는 도시의 *시/군/구* 의 정보를 이 변수에 담아 return 하게 된다.
    - 해당 변수에 값을 입력 할 때는 **append(contentsOf:)** 를 이용하여 sggNm 뒤에 원소를 추가한다.
- 만약 인자를 전달 받아 사용할 매개변수가 있을 시에는 selectCityNm 변수를 사용하지 않을 수 있다.

selectEmd() 는 인자를 받을 매개 변수는 없지만 String Array 를 반환한다.
- Struct Korea 에 **selectSggNm** 변수가 지정이 되어있지 않을 경우 원하는 값을 받을 수 없다.
- emdNm 은 String Array 형의 변수이다.
    - 해당 함수는 원하는 시/군/구 의 *읍/면/동* 정보를 이 변수에 담아 return 하게 된다.
    - selectSgg() 에서 데이터를 Array에 저장할 때의 방식을 사용하려 했으나 그러려면 한 줄로 작성된 String 을 다 떼어주는 선 작업이 필요로 했기에 사전 준비 없이 하나의 String 을 그대로 사용을 하기로 했다.
        - **append(contentsOf:separatedBy:)** 를 사용하여 해당 String 사이에 끼어있는 , 을 제거하고 Array 에 원소를 추가했다.
- emdBfNm 은 String 형의 변수이다.
    - 이는 emdNm 에서 append(contentsOf:separatedBy:) 를 사용하기 전에 String 데이터가 들어갈 변수이다.

왜 이렇게 만들었는가?
- 이 데이터를 공공데이터나 여러 기관 또는 인터넷 검색등을 통해 있는지 확인했으나 있어도 10% 정도 부족한 느낌으로 존재하는 경우가 많았으며 사전 작업이 많이 필요로 했기에 해당 방법으로 사용을 하고 있다.
- 해당 방법이 불편하거나 시정사항이 생긴다면 BJDAddressData2 의 파일로 새롭게 등록하도록 하겠다.


간단한 예시 코드
```
var korea:Korea = .init(selectCityNm: "도시", selectSggNm: "시군구", selectEmdNm: "읍면동")
korea.selectCityNm = "서울특별시"
let seoulSggList: [String] = korea.selectSgg()
print(seoulSggList)

///
["시/군/구", "강남구", "강동구", "강북구", "강서구", "관악구", "광진구", "구로구", "금천구", "노원구", "도봉구", "동대문구", "동작구", "마포구", "서대문구", "서초구", "성동구", "성북구", "송파구", "양천구", "영등포구", "용산구", "은평구", "종로구", "중구", "중랑구"]
///
```