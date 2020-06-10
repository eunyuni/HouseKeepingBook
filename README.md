# HouseKeepingBook
* 패스트 캠퍼스에서 진행한 팀 해커톤 프로젝트 1차
* 예산을 결정해서 1일 사용예산을 파악할 수 있는 부분과 스토어에 있는 앱은 1일 예산이 없는 점을 파악하여 차별화를 가질 수 있는 가계부를 만들고싶어서 개발



## Description

- 개발 기간: 2020.01.17 (1일)
- 참여 인원: iOS 3명
- 사용 기술
  - Language: Swift
  - FrameWork: UIKit
  - Library: JTAppleCalendar
- 담당 구현 파트
  - 영수증 UI
  - 세부목록 UI



## Views

![](https://user-images.githubusercontent.com/57210827/84137178-46999a80-aa87-11ea-8c76-9c71fa63777b.png)



## Implementation

![](https://user-images.githubusercontent.com/57210827/84150772-4c9a7600-aa9d-11ea-9de7-3877d81cb31d.gif)

- 달력
  - JTAppleCalendar library를 이용하여 달력 구현
  - 이달의 예산 설정 및 남은 예산 표현
  - 하루마다의 그날의 소비량에 따라 달력에 색으로 표시
  - 스크롤로 달력을 넘기는 기능
- 통계
  - 날짜별 소비 통계
    - 날짜 별로 얼마를 썻는지 표현
    - 날짜 별로 소비한 금액이 전체 소비금액의 몇 퍼센트인지 표현
  - 태그별 소비 통계
    - 태그 별로 얼마를 썻는지 표현
    - 태그별로 소비한 금액이 전체 소비금액의 몇 퍼센트 인지 표현
- Today
  - 일일 지출목록 표현
  - 지출목록 수정 기능(메모 추가)



## Trouble Shooting

* 영수증 화면과 지출등록하는 화면이 동일하여 두번그리지 않고 커스텀뷰를 이용하여 커스텀화
  * 버튼을 배열로 묶어서 자리배치
  * 버튼구성을 사용할 또다른곳에서 조금의 수정만 반영하여 재사용

```swift

    for (index, button) in tagButtons.enumerated() {
      switch index % 3 {
      case 0:
        button.trailingAnchor.constraint(equalTo: tagButtons[1].leadingAnchor, constant: -Padding.buttonXSpace).isActive = true
      case 1:
        button.centerXAnchor.constraint(equalTo: self.centerXAnchor).isActive = true
      default:
        button.leadingAnchor.constraint(equalTo: tagButtons[1].trailingAnchor, constant: Padding.buttonXSpace).isActive = true
      }
    }
    
    for button in tagButtons[0...2] {
      button.topAnchor.constraint(equalTo: self.topAnchor, constant: Padding.inset).isActive = true
    }
    
    for button in tagButtons[3...5] {
      button.topAnchor.constraint(equalTo: tagButtons[0].bottomAnchor, constant: Padding.buttonYSpace).isActive = true
    }
    
    for button in tagButtons[6...8] {
      button.topAnchor.constraint(equalTo: tagButtons[3].bottomAnchor, constant: Padding.buttonYSpace).isActive = true
      button.bottomAnchor.constraint(equalTo: self.bottomAnchor, constant: -Padding.inset).isActive = true
    }
  }
```



* 버튼클릭시 효과를 주기위하여 그림자효과를 추가했지만, 재사용하기에 코드가 반복되어 extension으로 확장

```swift
extension UIView {
  func shadow() {
    self.layer.shadowRadius = 8.0
    self.layer.shadowOpacity = 0.5
    self.layer.shadowOffset = .zero
    self.layer.shadowColor = UIColor.darkGray.cgColor
  }
  
  func unShadow() {
    self.layer.shadowRadius = 0
    self.layer.shadowOpacity = 0
    self.layer.shadowOffset = .zero
    self.layer.shadowColor = UIColor.clear.cgColor
  }
}
```

