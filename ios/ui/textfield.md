# TextField

Great article which digs deeper in how textfield works with iOS internally. [grokswift guide](https://grokswift.com/uitextfield/)

## Programmatic

[Stack Overflow](https://stackoverflow.com/questions/24710041/adding-uitextfield-on-uiview-programmatically-swift)

## Text Attributes

The general form for making and setting an attributed string is like this. You can find other common options below.

```swift
// create attributed string 
let myString = "Swift Attributed String" 
let myAttribute = [ NSAttributedString.Key.foregroundColor: UIColor.blue ] 
let myAttrString = NSAttributedString(string: myString, attributes: myAttribute)

// set attributed text on a UILabel 
myLabel.attributedText = myAttrString
```

[Source](https://stackoverflow.com/questions/24666515/how-do-i-make-an-attributed-string-using-swift)

### Color

We can set the blinking cursor color for the text field by setting the tintColor property.

```swift
// create attributed string 

let socialTextField = UITextField() 
socialTextField.tintColor = UIColor.yellow
```

## Delegates

You can import or override various delegate methods for your specific custom textfields and cater it towards different functionalities you want to have.

```swift
// View
protocol LoginViewDelegate: class {
    /// Informs that user wants to login with credentials
    func LoginViewDidReturnPassword(_ view: LoginView)
}

class LoginView: UIView {
        private lazy var passwordTextField: CustomTextField = {
        let field =  CustomTextField(textColor: .White,
                                     isSecuredEntry: true,
                                     contentType: .password,
                                     textFieldLabel: Texts.password.rawValue)
        field.CustomTextField.delegate = self
        field.CustomTextField.accessibilityLabel = Accessibility.password.rawValue.localized
        field.CustomTextField.tag = 1
        return field
    }()
}

// MARK: - UITextFieldDelegate Methods
extension LoginView: UITextFieldDelegate {
   public func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    if textField == passwordTextField.CustomTextField {
        print("Textfield value \(textField.text ?? "No Name")")
        delegate?.LoginViewDidReturnPassword(self)
    }
        textField.resignFirstResponder()
        return true
    }
}


// Controller Implementing Protocol

// MARK: - LoginViewDelegate Methods
extension LoginViewController: LoginViewDelegate {
    func LoginViewDidReturnPassword(_ view: LoginView) { }
}
```

### Unique Textfield

Identifying which textfield belongs to can be done utilizing tags or even basic `==` operator.

This [StackOverflow post](https://stackoverflow.com/questions/50465748/swift-4-identifying-only-one-text-field-as-delegate-for-editingdidend-etc) explains it better.

## Validation

Validation is needed for checking input fields like email and password or enforcing different policies on the user with available input options.

[Small article Validating](https://medium.com/swift2go/a-better-approach-to-text-field-validations-on-ios-81bd87598070)

## Navigation

Form like navigation from one text field to next textfield [SO](https://stackoverflow.com/questions/1347779/how-to-navigate-through-textfields-next-done-buttons) [Hacking With Swift](https://www.hackingwithswift.com/example-code/uikit/how-to-move-to-the-next-uitextfield-when-the-user-presses-return)

But I chose a different approach with custom Text fields and just directly sent the responder with specific text field.

```swift
class LoginView: UIView {
        private lazy var emailTextField: CustomTextField = {
         let field =  CustomTextField(keyboard: .emailAddress,
                                      textColor: .White,
                                      contentType: .emailAddress,
                                      textFieldLabel: Texts.emailLabel.rawValue)
        field.CustomTextField.delegate = self
        field.CustomTextField.accessibilityLabel = Accessibility.email.rawValue.localized
        field.CustomTextField.returnKeyType = .next
        return field
    }()

        private lazy var passwordTextField: CustomTextField = {
        let field =  CustomTextField(textColor: .White,
                                     isSecuredEntry: true,
                                     contentType: .password,
                                     textFieldLabel: Texts.password.rawValue)
        field.CustomTextField.delegate = self
        field.CustomTextField.accessibilityLabel = Accessibility.password.rawValue.localized
        field.CustomTextField.tag = 1
        return field
    }()
}

// MARK: - UITextFieldDelegate Methods
extension LoginView: UITextFieldDelegate {

public func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    if textField == emailTextField.CustomTextField {
        passwordTextField.CustomTextField.becomeFirstResponder()
    } else if textField == passwordTextField.CustomTextField {
        textField.resignFirstResponder()
        delegate?.ReturnPassword(self)
    }
    return true
}
}
```

## Behaviors

### UserInteractionEnabled vs Enabled

If we want the textfield to be user intractable which is by default turned on.

* IsUserInteractionEnabled doesn’t change any background of the default textfield.
* isEnabled does change the background opacity to minimum and it results into a darker grayish disabled view.

```swift
private lazy var emailTextField: UITextField = {
       let field = UITextField()
       field.text = "Kautilya Save"
       field.isUserInteractionEnabled = false
       field.isEnabled = false
       field.backgroundColor = .gray
       return field
    }()
```

This behavior is valid until the custom UITextField class hasn’t been defined with its background color property.

> self.backgroundColor = .clear

Then you would have to override the custom UITextField object with the backgroundColor property accordingly

> emailTextField.backgroundColor = isEnabled ? .clear : .gray

[SO](https://stackoverflow.com/questions/29791644/disabling-user-input-for-uitextfield-in-swift)

