# Input Field

## Validation

Check for empty string

> if \(inputFieldGameObjectRef.textComponent.text == ""\){ }

Equals with another input field text

```csharp
if (EmailAddress.text != ConfirmEmailAddress.text)
{
 EmailAddress.placeholder.color = Color.red;
 ConfirmEmailAddress.placeholder.color = Color.red;
}
```

## Input type

You can specify which input type should be for the input field in the attribute inspector in Unity application.

[Source](https://docs.unity3d.com/560/Documentation/Manual/script-InputField.html)

