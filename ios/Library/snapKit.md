# SnapKit


## Errors


### Constraints

```
*** Terminating app due to uncaught exception 'NSGenericException', reason: 'Unable to activate constraint with anchors <NSLayoutDimension:0x60000036e080 "UIImageView:0x7ffc0384aa70.height"> and <NSLayoutDimension:0x60000036e0c0 "WearWorks.Label:0x7ffc03819920'Sign Up'.height"> because they have no common ancestor.  Does the constraint or its anchors reference items in different view hierarchies?  That's illegal.'
*** First throw call stack:
```



``` reason: 'Unable to activate constraint with anchors <NSLayoutYAxisAnchor:0x6000003ad780 "WearWorks.TextField:0x7ff1fcf25d20.top"> and <NSLayoutYAxisAnchor:0x600000349080 "WearWorks.Label:0x7ff1fce40f80'Create an account to save...'.bottom"> because they have no common ancestor.  Does the constraint or its anchors reference items in different view hierarchies?  That's illegal.'
*** First throw call stack:
```

My understanding: 

This time the constraint was not available at runtime as we had commented the code & snap kit didn’t throw any errors due to maybe the library works runtime constraint execution or unwrapping but it turns out that code was commented so null pointer reference to begin with.

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

Here *descriptionLabel.snp.bottom* can’t be referenced as it is commented in the code.