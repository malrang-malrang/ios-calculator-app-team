# iOS-calculator-app
> 프로젝트 기간 2022.03.28 ~ 2022.04.01  
>팀원 : [malrang](https://github.com/kinggoguma), [donnie](https://github.com/westeastyear)   
>리뷰어 : [도미닉](https://github.com/AppleCEO)  

- [프로젝트 규칙](#프로젝트-규칙)
- [실행화면](#실행화면)
- [UML](#uml)
- [STEP 1 기능 구현](#step-1-기능-구현)
    + [고민했던 것들](#고민했던-것들)
    + [배운 개념](#배운-개념)
    + [PR 후 개선사항](#pr-후-개선사항)
 - [STEP 2 기능 구현](#step-2-기능-구현)
    + [고민했던 것들](#고민했던-것들)
    + [배운 개념](#배운-개념)
    + [PR 후 개선사항](#pr-후-개선사항)

## 프로젝트 규칙
### 활동시간
>월, 화, 목, 금 : 11시 ~ 22시
>수요일 : 개인공부

>점심시간 : 13시 ~ 14시
>저녁시간 : 18시 ~ 20시

### TIL 깃커밋 메세지
>✅[chore]: 코드 수정, 내부 파일 수정.  
✨[feat]: 새로운 기능 구현.  
📐[style]: 스타일 관련 기능.(코드 포맷팅, 세미콜론 누락, 코드 자체의 변경이 없는 경우)  
➕[add]: Feat 이외의 부수적인 코드 추가, 라이브러리 추가, 새로운 파일 생성 시.  
🔨[fix]: 버그, 오류 해결.  
⚰️[del]: 쓸모없는 코드 삭제.  
📝[docs]: README나 WIKI 등의 문서 개정.  
💄[mod]: storyboard 파일,UI 수정한 경우.  
✏️[correct]: 주로 문법의 오류나 타입의 변경, 이름 변경 등에 사용합니다.  
🚚[move]: 프로젝트 내 파일이나 코드의 이동.  
⏪️[rename]: 파일 이름 변경이 있을 때 사용합니다.  
⚡️[improve]: 향상이 있을 때 사용합니다.  
♻️[refactor]: 전면 수정이 있을 때 사용합니다  
🔀[merge]: 다른브렌치를 merge 할 때 사용합니다.  

## 실행화면
![Mar-27-2022 16-59-31](https://user-images.githubusercontent.com/88717147/160272509-a37b9cef-ff23-47a8-98ea-4f1c99a0f519.gif)

## UML

## STEP 1 기능 구현
- enum CalculatorNameSpace
    - Calculator 프로젝트에서 사용될 하드코딩될 문자들을 담아둔 NameSpace
- class CalculatorNode
    - 양방향 Linked-List 구현에 필요한 Value와 next, previous 값을 가지고 있는 노드 구현
- class CalculatorLinkedList
    - CalculatorNode 를 활용하여 값을 저장하고 제거할수 있는 자료구조
    - append() CalculatorLinkedList 에 저장된 값의 마지막에 Node를 저장하는 메서드
    - removeFirst() CalculatorLinkedList 에 저장된 처음 Node 를 제거하고 값을 반환 하는 메서드
    - removeAll() 현재 저장된 Node를 모두 제거하는 메서드
- struct CalculatorQueue
    - LinkedList 를 Queue 자료구조로 사용할수 있도록 정의해둔 타입
    - enqueue() LinkedList 의 append() 를 호출하여 Node에 값을 저장하는 메서드
    - dequeue() LinkedList 의 removeFirst() 를 호출하여 LinkedList 에 저장된 처음 Node를 제거하는 메서드
    - allClear() LinkedList 의 removeAll() 을 호출하여 LinkedList 에 저장된 모든 Node를 제거하는 메서드
- enum Operator
    - calculate() Operator case 의 값에 따라 매개변수들을 연산하는 메서드
    - add() 매개변수를 2개 받아 값을 더해주는 메서드
    - sub() 매개변수를 2개 받아 값을 차감하는 메서드
    - divide() 매개변수를 2개 받아 값을 나눠주는 메서드
    - multiply() 매개변수를 2개 받아 값을 곱해주는 메서드
- struct Formula
    - result() 저장된 연산자와 피연산자를 활용해 값을 연산해주는 메서드
- enum ExpressionParser
    - parse() String 타입의 매개변수를 연산자와 피연산자로 구분하여 저장된 Formula 를 반환하는 메서드
    - componentsByOperators() String 타입의 값을 공백을 기준으로 분리시켜주는 메서드
## 고민했던 것들
1. removeFirst 메서드 에서 현재 노드를 제거하고 노드가 가지고있던 값을 반환해야함
2. Calculator 프로젝트에서 사용될 네임스페이스의 이름

## 배운 개념
- unit-test
- 자료구조 Queue
- generic
- linked-List
- defer
- forEach 내부에서의 return 구문
- else 를 남발하였을때 생기는 불편함
- while let 을 이용한 옵셔널바인딩
- early return
- early continue
- early break

## PR 후 개선사항
1. removeFirst 의 defer 구문
> defer 구문을 활용해 제거될 head 의 value 를 제거되기전에 반환후 제거되도록 사용한 코드였으나 defer 구문이 사용됨으로 이해하기 어려운 코드였다.
> 제거될 head 의 value 를 임시로 상수에 저장한후 head 를 제거한후 임시 저장한 상수를 반환하도록 변경함.

**변경전 코드**
```swift
func removeFirst() -> T? {
        if isEmpty {
            return nil
        }
        defer {
            head = head?.next
        }
        return head?.value
    }
```
**변경후 코드**
```swift
 func removeFirst() -> T? {
        if isEmpty {
            return nil
        }
        let removeHead = head?.value
        head = head?.next
        
        return removeHead
    }
```

2. Calculator 의 네임 스페이스 이름을 CalculatorEtc -> CalculatorNameSpace 로 변경함.
> 네임스페이스 에서 사용되는 값들을 한번에 묶어 표현할수 있는 단어가 떠오르지 않아 NameSpace 라는 단어를 표기하여 사용하도록 변경 하였다.
## STEP 2 기능 구현
- CalculatorViewController
     - didTapAllClearButton() 입력하여 저장된 숫자와 연산자들의 정보를 제거, 추가된 스택뷰를 제거 하는 메서드
    - didTapClearEntryButton() 가장 마지막 입력된 숫자를 제거하는 메서드
    - didTapPositiveNegativeConversionButton() 입력된 숫자의 부호를 바꾸어 저장하는 메서드
    - didTapOperandButtons() 계산기 UI 의 숫자 버튼을 누르면 해당 숫자가 저장되는 메서드
    - didTapSingleDotButton() 계산기 UI 의 소수점 버튼을 누르면 입력된 숫자 뒤에 소수점이 붙는 메서드
    - didTapOperatorButtons() 계산기 UI 의 연산자 버튼을 누르면 해당 연산자가 저장되고 입력된 값과 연산자를 지역 프로퍼티인 confirmedFormula 에 저장 한후 해당 값들이 스크롤뷰 내부의 스택뷰가 추가되는 메서드
    - didTapEqualSignButton() 지금까지 입력된 숫자와 연산자를 입력받아 계산하여 결과를 보여주는 메서드
- CalculatorViewController extention
    - initializeCalculatorHistory() 입력되어 저장된 숫자와 연산자를 제거해주는 메서드
    - isValidTemporaryOperandTextDigitsLessFifteenCount() 현재 입력된값이 Double 타입의 유효자리숫자 보다 많은지 적은지 Bool 값을 반환하는 메서드
    - isValidFirstInputNonZero() 입력되어 저장되어있는 값이 0 일때 현재 입력한 값이 0,00 인지 Bool 값을 반환하는 메서드
    - numberFormatter() 입력된 값을 numberFormatter 에 설정한 스타일로 변경해주는 메서드
    - validateTemporaryOperandTextConditionAndChangeValue() 현재 입력한 값을 조건에 따라 분류하여 Label.text 에 할당해주는 메서드
    - updateTemporaryOperandText() 입력된 값을 현재 저장하고있던 값에 업데이트(대체) 해주는 메서드
    - appendTemporaryOperandText() 입력된 값을 현재 저장하고 있던 값에 추가해주는 메서드
    - hasNotIncludedSingleDot() 저장된 값에 소수점이 포함되어있는지 Bool 값을 반환해주는 메서드
    - appendArrangedStackView() 저장된 값과 입력한 연산자 값을 파라미터로 받아 스크롤뷰 내부의 스택뷰를 추가해주는 메서드
- UIScrollView extention
    - scrollToBottom() 스택뷰가 추가될경우 스크롤뷰가 추가된 높이만큼 viewPort 를 내려주는 메서드

## 고민했던 것들
1. UI를 통해 입력된 값을 저장하는방법
2. 저장된 숫자와 연산자를 스택뷰에 추가하는방법
3. 저장된 숫자와 연사자를 연산하는 방법
4. 입력값에 소수점이 추가되었을 경우 넘버포메터를 적용하지 않는방법
5. 저장된 값에 부호를 변경하는 방법
> 부호를 변경하는 버튼을 클릭시 값의 부호를 어떻게 변경해야할지 고민이 많았습니다. 기존 짜두었던 코드>에서 진행해야 했기 때문에 잘못 건드릴 경우 사이드 이펙트가 발생하여 가장 어려웠던 부분이다.
>
>처음 진행한 방법은 현재 String 값을 Double 타입으로 변경해 -1을 곱해주어(* -1) 부호를 변경한>후 다시 String 값으로 변환하는 방법을 사용했습니다.
>
>하지만 타입변환을 하는과정에 .0 이라는 소수점 값이 생기게 되어 이를 해결할수 있는 방법을 많이 고민 >하였으나 -1을 곱하는 방법에서 기존 String 값에 "-" 을 추가하거나 제거하는 방식으로 변경하였다.

**변경전 코드**
>입력된 값을 Double 타입으로 변환후 -1을 곱해주어 부호를 변경한뒤 다시 String 타입으로 변환
```swift
    let converteDouble = Double(temporaryOperandText) ?? CalculatorNameSpace.singleZero
    temporaryOperandText = String(converteDouble * -1)
    operandsLabel.text = CalculatorNameSpace.negativeSign + operandsLabelText
```
**변경후 코드**
>입력된 값의 앞에 위치한 문자가 "-" 일경우 제거
>입력된 값의 첫번째 위치에 "-" 추가
```swift
    if temporaryOperandText.hasPrefix(CalculatorNameSpace.negativeSign) {
        temporaryOperandText.removeFirst()
        operandsLabelText.removeFirst()
        operandsLabel.text = operandsLabelText
        return
        }
    temporaryOperandText = CalculatorNameSpace.negativeSign + temporaryOperandText
    operandsLabel.text = CalculatorNameSpace.negativeSign + operandsLabelText
    }
```

## 배운 개념
1. AutoLayOut
2. ScrollView
3. StackView
4. Formatter
5. NumberFormatter
6. frame 과 bound 의 차이
7. Mark 활용법

## PR 후 개선사항
