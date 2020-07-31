# Override Defaults

## Remove underline in links with CSS

[Source](https://stackoverflow.com/questions/2789703/remove-stubborn-underline-from-link) As I expected, you are not applying text-decoration: none; to an anchor \(.boxhead a\) but to a span element \(.boxhead\).

Try this:

```css
.boxhead a {
    color: #FFFFFF;
    text-decoration: none;
}
```

