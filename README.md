# jwp-racingcar

## 웹 요청 / 응답 구현하기

### 경주 게임 시작
WebController
- [x] 게임 play Post 요청 받기
  - [x] 자동차 이름 분리
  - [x] 자동차 객체 생성
  - [x] 게임 결과 반환 (winners, racingCars)

Service
- [x] 게임 플레이

Dto
- [x] CarDto
- [x] RequestDto
- [x] ResponseDto

## DB 연동하기
- [x] 플레이 횟수, 플레이어 별 최종 이동거리, 우승자, 플레이한 날짜/시간 저장

## 리팩토링, 공부할 내용
- [x] 사용자가 입력한 값에 대한 Validation 구현
  - [x] 시도횟수는 양수여야 한다.
  - [x] 같은 게임에 한해서 차 이름은 중복될 수 없다.
- [x] 잘못된 값에 대한 예외처리
- [x] CAR_RESULT가 is_winner 컬럼을 갖도록 테이블 및 Dao 수정
  - CAR_RESULT가 is_winner 컬럼을 가짐으로써 조인이 필요 없어졌다. 게임 이력 조회의 책임 GameDao -> CarDao로 이동

## 궁금한 내용
- [ ] CAR_RESULT와 PLAY_RESULT를 조인해서 조회하는 책임은 어떤 Dao 클래스가 가지는 것이 좋을까?
- [ ] 사용자의 입력값에 대한 유효성 검사는 어떤 계층에서 이뤄져야 할까?
- [ ] 현재는 순수 자바 코드로 작성된 도메인 객체가 있고, 해당 도메인에서 유효성 검사가 이뤄지고 있다. 보통은 어떻게 유효성 검사를 할까?
- [x] PLAY_RESULT의 winners column 제거
- [ ] DB에 종속적이지 않은 테스트를 작성하는 방법

## 2단계 요구사항
- [x] 게임 플레이 이력 조회 API 구현
  - [x] Request: GET /plays HTTP/1.1
  - [x] Response:
    {
      "winners": "브리",
      "racingCars": [
        {
          "name": "브리",
          "position": 6
        },
        {
          "name": "토미",
          "position": 4
        },
        {
          "name": "브라운",
          "position": 3
        }
      ]
    }
  - [x] 응답용 DTO 필요 -> List<ResponseDto>
    - 뷰에서 받는 데이터에 맞추기 위해 새로운 DTO 클래스를 생성하지 않고 List를 반환하는 것으로 결정
  - [x] ResponseDto 클래스명 변경 필요해보임
  - [x] SELECT 쿼리 작성
- [x] 기존 기능 수정 - 출력 방식 수정
  - [x] console application에서 플레이의 중간 과정을 출력하는 로직을 제거
  - [x] console application에서 web application과 동일하게 우승자와 player 별 최종 이동거리를 출력하도록 수정
- [x] 리팩터링 - 중복 코드 제거
  - [x] 두 application은 입출력과 데이터 저장 방식을 제외하고는 내부 비즈니스 로직은 동일하다.
  - [x] 두 application의 비즈니스 로직은 새로운 객체를 도출 하여 중복 제거를 할 수 있다.
