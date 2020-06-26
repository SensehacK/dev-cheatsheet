# iOS View Controllers



## Creation

Different types of View controller can be utilized.
We would initialize view controller using storyboard and setting the controller in the inspector.

The parent view will perform a segue and call upon the storyboard using Storyboard references and storyboard name.

## Present

This would be better explained using iOS Segues doc as we would dive more deep into that doc about creating segues and linking them differently.

## Dismiss


Dismissing Child view controller could be done using various methods depending on how it was created.

Navigation controller needs pop method to dismiss
> self.navigationController?.popViewController(animated: true)

> Normal View controller uses just dismiss method.
> self.dismiss(animated: true, completion: nil)

