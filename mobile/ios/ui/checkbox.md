# CheckBox

## Implementation

Programmatically making a button toggle between active and inactive state using an checkmark image.

### Custom UIButton Class

```swift
import UIKit

class CheckMarkButton: UIButton {

    // MARK: - Private Properties
    private var isSet: Bool

    // MARK: - Inits
    init(isSet: Bool = false) {
        self.isSet = isSet
        super.init(frame: .zero)
        setup()
    }

    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    /// Changes icon of toggle Checkmark
    func toggleCheckmark() {
       isSet = !isSet
        if isSet {
            setImage(Icons.checkActive, for: .normal)
        } else {
            setImage(nil, for: .normal)
        }
    }

}

// MARK: - Life Cycle Methods
extension CheckMarkButton {

    override func layoutSubviews() {
        super.layoutSubviews()
        round(with: Constants.cornerRadius, corners: [.allCorners])
    }

}

// MARK: - Private Instance Methods
private extension CheckMarkButton {

    /// Sets all properties
    func setup() {
        if isSet {
            setImage(Icons.checkActive, for: .normal)
        } else {
            setImage(nil, for: .normal)
        }
        backgroundColor = .wwWhite
    }

}

private extension CheckMarkButton {

    struct Constants {

        private init() {}

        static let cornerRadius: CGFloat = 12

    }

    struct Icons {

        private init() {
        }

        static let checkActive = #imageLiteral(resourceName: "checkmarkYes")
        static let checkInactive = #imageLiteral(resourceName: "checkmarkNo")

    }

}
```

Good sources [SO](https://stackoverflow.com/questions/29117759/how-to-create-radio-buttons-and-checkbox-in-swift-ios)

[Medium Simple Checkbox](https://medium.com/swift-india/simple-checkbox-component-in-ios-311a865c0b02)

Usage of the extension with protocol delegate coordinator pattern with programmatic UI.

### View Class

```swift
protocol RegisterViewDelegate: class { 

        /// Informs that user wants to specify date of birth
    func registerViewDidTapCheckmark(_ view: RegisterView)

}

class UserProfileView: UIView {

    // MARK: - Weak Properties
    weak var delegate: UserProfileViewDelegate?

        private lazy var checkmarkButton: CheckMarkButton = {
        let button = CheckMarkButton(isSet: false)
        button.addTarget(self, action: #selector(checkmarkButtonTapped(sender:)), for: .touchUpInside)
        return button
    }()

       /// Reacts to back button being tapped
    @objc func checkmarkButtonTapped(sender: CheckMarkButton) {
        print("Check mark active")
        sender.toggleCheckmark()
        delegate?.registerViewDidTapCheckmark(self)
    }

}
```

### ViewController Class

```swift
class RegisterViewController: UIViewController {

        // MARK: - Properties
    var isCheckmark: Bool?

    // MARK: - Overridden Properties
    override var preferredStatusBarStyle: UIStatusBarStyle {
        return .lightContent
    }

    // MARK: - Lazy Properties
    private(set) lazy var coordinator = RegisterCoordinator(dataSource: registerView.content)

    private(set) lazy var registerView: RegisterView = {
        let view = RegisterView()
        view.delegate = self
        view.button.isEnabled = false
        return view
    }()

}

// MARK: - Life Cycle Methods
extension RegisterViewController {

    override func loadView() {
        view = registerView
        isCheckmark = false
    }

    override func viewDidLoad() {
        super.viewDidLoad()
    }

    open override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
    }
}

// MARK: - RegisterViewDelegate Methods
extension RegisterViewController: RegisterViewDelegate {

    func registerViewDidTapCheckmark(_ view: RegisterView) {
        isCheckmark = !(isCheckmark ?? false)
        enableRegisterButton()
    }

}

// MARK: - Private Instance Methods
private extension RegisterViewController {

    // Enables the Register Button
    func enableRegisterButton() {
        let isEnabled = isCheckmark != false
        registerView.button.isEnabled = isEnabled
    }

}
```

