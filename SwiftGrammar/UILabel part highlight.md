# UILabel part highlight

---

- UIKit 으로 구현해볼게요.

## **NSMutableAttributedString 적용**

---

```swift
private let pointLabel = UILabel()
// NSMutableAttributedString Type으로 바꾼 text를 저장
let attributedStr = NSMutableAttributedString(string: pointLabel.text!)
// text의 range 중에서 "Bonus"라는 글자는 UIColor를 blue로 변경
attributedStr.addAttribute(.foregroundColor, value: UIColor.blue, range: (pointLabel.text! as NSString).range(of: "Bonus"))
// text의 range 중에서 "Point"라는 글자는 UIColor를 orange로 변경
attributedStr.addAttribute(.foregroundColor, value: UIColor.orange, range: (pointLabel.text! as NSString).range(of: "Point"))
// 설정이 적용된 text를 label의 attributedText에 저장
pointLabel.attributedText = attributedStr
```

## part highlight 다양한 속성들

---

- font, font size 등 다양한 것들 을 할 수 있음.

```swift
static let cursor: NAttributedString. Key The value of this attribute is an NSCursor object. The default value is the cursor
returned by the iBeam method
static let expansion: NSAttributedString.Key
static let font: NSAttributedString.Key
static let foregroundColor: NSAttributedString.Key
static let glyphInfo: NSAttributedString. Key
The name of an NSGlyphInfo object.
static let kern: NSAttributedString.Key
static let ligature: NSAttributedString.Key
static let link: NAttributedString.Key
static let markedClauseSegment: NSAttributedString.Key
static let obliqueness: NAttributedString.Key
static let paragraphStyle: NSAttributedString.Key
static let shadow: NAttributedString. Key
```