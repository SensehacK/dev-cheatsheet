# SnapKit

## Errors

### Constraints

```text
*** Terminating app due to uncaught exception 'NSGenericException', reason: 'Unable to activate constraint with anchors <NSLayoutDimension:0x60000036e080 "UIImageView:0x7ffc0384aa70.height"> and <NSLayoutDimension:0x60000036e0c0 "WearWorks.Label:0x7ffc03819920'Sign Up'.height"> because they have no common ancestor.  Does the constraint or its anchors reference items in different view hierarchies?  That's illegal.'
*** First throw call stack:
```

\`\`\` reason: 'Unable to activate constraint with anchors and because they have no common ancestor. Does the constraint or its anchors reference items in different view hierarchies? That's illegal.' _\*_ First throw call stack:

```text
My understanding: 

This time the constraint was not available at runtime as we had commented the code & snap kit didn’t throw any errors due to maybe the library works runtime constraint execution or unwrapping but it turns out that code was commented so null pointer reference to begin with.
```

```swift
/*
        container.addSubview(descriptionLabel)
        descriptionLabel.snp.makeConstraints { maker in
            maker.leading.trailing.equalToSuperview()
            maker.top.equalTo(titleLabel.snp.bottom).offset(Paddings.descriptionTop)
        }
        */

        container.addSubview(fullNameTextField)
        fullNameTextField.snp.makeConstraints { maker in
            maker.leading.trailing.equalToSuperview()
            maker.top.equalTo(descriptionLabel.snp.bottom).offset(Paddings.fullNameTop)
        }
```

Here _descriptionLabel.snp.bottom_ can’t be referenced as it is commented in the code.

Parent subview not present error:

```text
reason: 'NSLayoutConstraint for <UIView: 0x7ff16cc39bf0; frame = (0 0; 0 0); layer = <CALayer: 0x60000012d5e0>>: A multiplier of 0 or a nil second item together with a location for the first attribute creates an illegal constraint of a location equal to a constant. Location attributes must be specified in pairs.'
```

So this happens if the snap kit element is referencing on a certain parent object which hasn’t been instantiated or called upon before executing the child object.

