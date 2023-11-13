
## Intro

It is kind of stream or chain type of pattern where you can extract complexity and allow better mutability while creating an object to interact with. It definitely helps when you're designing an API for consumers on the framework / library side of things.


## Syntax

Non Builder code
```swift
let view = ArticleView()
view.titleLabel.text = article.title
view.subtitleLabel.text = article.subtitle
view.imageView.image = article.image
```

Builder pattern code
```swift
let view = ArticleViewBuilder()
    .withTitle(article.title)
    .withSubtitle(article.subtitle)
    .withImage(article.image)
    .build()
```
Code snippet and builder pattern in swift by [Swift by Sundell](https://www.swiftbysundell.com/articles/using-the-builder-pattern-in-swift/)
