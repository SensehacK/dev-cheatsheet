# Date Picker

## Implementation

Programmatically making a text field open up Date picker with two selectors of able to cancel the picker and save the date from the picker.

### Extension

```swift
import UIKit
extension UITextField {

    func setInputViewDatePicker(target: Any, selector: Selector) {
        // Create a UIDatePicker object and assign to inputView
        let screenWidth = UIScreen.main.bounds.width
        let datePicker = UIDatePicker(frame: CGRect(x: 0, y: 0, width: screenWidth, height: 216))
        datePicker.datePickerMode = .date 
        self.inputView = datePicker 

        // Create a toolbar and assign it to inputAccessoryView
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

[Swift Dev Center](https://www.swiftdevcenter.com/uidatepicker-as-input-view-to-uitextfield-swift/)

Usage of the extension with protocol delegate coordinator pattern with programmatic UI.

### View Class

```swift
protocol UserProfileViewDelegate: class { 

        /// Informs that user wants to specify date of birth
    func userProfileViewDidTapDateOfBirth(_ view: UserProfileView, textField: UITextField)

}

class UserProfileView: UIView {

    // MARK: - Weak Properties
    weak var delegate: UserProfileViewDelegate?

        private lazy var dateOfBirthTextField: TextField = {
                let field = TextField(placeholder: Texts.dateOfBirth.rawValue,
                                      keyboard: UIKeyboardType.alphabet,
                                      contentType: .name)
                field.textField.accessibilityLabel = Accessibility.dateOfBirth.rawValue.localized
                field.textField.setInputViewDatePicker(target: self, selector: #selector(datePickerDoneButtonTapped))
                return field
            }()



        @objc func datePickerDoneButtonTapped() {
                delegate?.userProfileViewDidTapDateOfBirth(self, textField: dateOfBirthTextField.textField)
            }


}
```

### ViewController Class

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

    func userProfileViewDidTapDateOfBirth(_ view: UserProfileView, textField: UITextField) {
        if let datePicker = textField.inputView as? UIDatePicker {
            let dateformatter = DateFormatter() 
            dateformatter.dateStyle = .medium 
            textField.text = dateformatter.string(from: datePicker.date)
        }
        textField.resignFirstResponder()
    }

}
```

## Properties

Setting Minimum or Maximum date in the picker view

```swift
let datePicker = UIDatePicker(frame: CGRect(x: 0, y: 0, width: screenWidth, height: 216))
        datePicker.datePickerMode = .date
        datePicker.minimumDate = Calendar.current.date(byAdding: .year, value: -150, to: Date())
        datePicker.maximumDate = Calendar.current.date(byAdding: .year, value: -18, to: Date())
        self.inputView = datePicker
```

[StackOverflow](https://stackoverflow.com/questions/10494174/minimum-and-maximum-date-in-uidatepicker)



## Formatting 