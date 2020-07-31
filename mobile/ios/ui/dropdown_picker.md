# Dropdown Picker

### Implementation

Programmatically making a text field open up Dropdown picker with two selectors of able to cancel the picker and save the dropdown text from the picker.

#### Extension

```swift
import UIKit
extension UITextField {

   func loadDropdownData(data: [String], selector: Selector) {
        self.inputView = PickerView(pickerData: data, dropdownField: self)

        // Create a toolbar and assign it to inputAccessoryView
        let screenWidth = UIScreen.main.bounds.width
        let toolBar = UIToolbar(frame: CGRect(x: 0.0, y: 0.0, width: screenWidth, height: 44.0))
        let flexible = UIBarButtonItem(barButtonSystemItem: .flexibleSpace, target: nil, action: nil)
        let cancel = UIBarButtonItem(title: "Cancel", style: .plain, target: nil, action: #selector(CancelButtonTapped))
        let barButton = UIBarButtonItem(title: "Done", style: .plain, target: target, action: selector)
        toolBar.setItems([cancel, flexible, barButton], animated: false)
        self.inputAccessoryView = toolBar
    }

    @objc func CancelButtonTapped() {
        self.resignFirstResponder()
    }

}
```

Great article, learned a lot about how events work, toolbar creation on top of picker view. Flexible space in between, input field accessoryView methods.

[Source](https://www.credera.com/blog/custom-application-development/creating-a-dropdown-field-in-swift-for-ios/)

Usage of the extension with protocol delegate coordinator pattern with programmatic UI.

#### View Class

```swift
protocol UserProfileViewDelegate: class { 

        /// Informs that user wants to specify Dropdown of birth
    func userProfileViewDidTapDropdown(_ view: UserProfileView, textField: UITextField)

}

class UserProfileView: UIView {

    // MARK: - Weak Properties
    weak var delegate: UserProfileViewDelegate?

        private lazy var genderTextField: TextField = {
                let field = TextField(placeholder: Texts.gender.rawValue,
                              keyboard: UIKeyboardType.alphabet,
                              contentType: .name)
        field.textField.accessibilityLabel = Accessibility.gender.rawValue.localized
        field.textField.loadDropdownData(data: genderTypes, selector: #selector(genderPickerDoneButtonTapped))
        return field
            }()

        @objc func genderPickerDoneButtonTapped() {
                genderTextField.textField.resignFirstResponder()
            }
}
```

#### ViewController Class

```swift
class UserProfileViewController: UIViewController {

    // MARK: - Overridden Properties
    override var preferredStatusBarStyle: UIStatusBarStyle {
        return .lightContent
    }

    // MARK: - Lazy Properties
    private(set) lazy var coordinator = UserProfileCoordinator(dataSource: userProfileView.content)

    private(set) lazy var userProfileView: UserProfileView = {
        let view = UserProfileView()
        view.delegate = self
        return view
    }()

}

// MARK: - Life Cycle Methods
extension UserProfileViewController {

    override func loadView() {
        view = userProfileView
    }

    override func viewDidLoad() {
        super.viewDidLoad()
    }

    open override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
    }
}

// MARK: - UserProfileViewDelegate Methods
extension UserProfileViewController: UserProfileViewDelegate {

    func userProfileViewDidTapDropdown(_ view: UserProfileView, textField: UITextField) {
        if (true) {
            // TODO: Parsing the text or just updating the UI based on the selected input from the dropdown list.
            } 
        textField.resignFirstResponder()
    }

}
```

