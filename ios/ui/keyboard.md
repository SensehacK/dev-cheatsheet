# Keyboard

```swift
import UIKit

enum KeyboardAppearance {

    case visible(height: CGFloat)
    case invisible

}

protocol KeyboardHandlerDelegate: class {

    /// Informs that appearance of keyboard has changed
    func keyboardHandler(_ handler: KeyboardHandler, didUpdate appearance: KeyboardAppearance)

}

class KeyboardHandler {

    // MARK: - Properties
    var initialBottomInset: CGFloat?

    // MARK: - Weak Properties
    weak var delegate: KeyboardHandlerDelegate?

    // MARK: - Private Properties
    private let scrollView: UIScrollView?
    private let notificationCenter: NotificationCenter

    // MARK: - Private Set Properties
    private (set) var appearance: KeyboardAppearance = .invisible

    // MARK: - Inits
    init(scrollView: UIScrollView? = nil, notificationCenter: NotificationCenter = .default) {
        self.scrollView = scrollView
        self.notificationCenter = notificationCenter
        self.initialBottomInset = scrollView?.contentInset.bottom
    }

    // MARK: - Public Instance Methods
    func observe() {
        notificationCenter.addObserver(self, selector: #selector(keyboardWillAppear), name: UIResponder.keyboardWillShowNotification, object: nil)
        notificationCenter.addObserver(self, selector: #selector(keyboardWillDisappear), name: UIResponder.keyboardWillHideNotification, object: nil)
    }

}

// MARK: - Private Instance Methods
private extension KeyboardHandler {

    /// Reacts to keyboard being showed. Changes scrollView's object bottom inset to desired keyboard height
    @objc func keyboardWillAppear(_ notification: NSNotification) {
        if let rect = notification.userInfo?[UIResponder.keyboardFrameEndUserInfoKey] as? NSValue {
            let height: CGFloat = rect.cgRectValue.height
            scrollView?.contentInset.bottom = height
            appearance = .visible(height: height)
            delegate?.keyboardHandler(self, didUpdate: appearance)
        }
    }

    /// Reacts to keyboard being showed. Changes scrollView's object bottom inset to 0
    @objc func keyboardWillDisappear(_ notification: NSNotification) {
        if let initialBottomInset = initialBottomInset, let scrollView = scrollView {
            scrollView.contentInset.bottom = initialBottomInset
        }
        appearance = .invisible
        delegate?.keyboardHandler(self, didUpdate: appearance)
    }

}
```

## Utilization

```swift
class UserProfileView: UIView {

    // MARK: - Lazy Properties
    private lazy var keyboardHandler = KeyboardHandler(scrollView: scrollView)

     // MARK: - Inits
    init() {
        super.init(frame: .zero)
        keyboardHandler.observe()
    }
}
```



## Initialization


## Delegates

> @objc func keyboardWillAppear
> @objc func keyboardWillDisappear

## Customizability





[Dismiss Keyboard](https://medium.com/@KaushElsewhere/how-to-dismiss-keyboard-in-a-view-controller-of-ios-3b1bfe973ad1)

Custom InputField Dismiss Keyboard

[Stack Overflow](https://stackoverflow.com/questions/36001119/dismissing-keyboard-on-custom-uitextfield)

## Dismiss on InActive Tap

[TutorialsPoint](https://www.tutorialspoint.com/how-do-you-hide-the-onscreen-keyboard-in-ios-app)

https://stackoverflow.com/questions/24126678/close-ios-keyboard-by-touching-anywhere-using-swift?rq=1

## Customization

[Text Return custom](https://stackoverflow.com/questions/976950/change-text-of-return-keyboard-button)

