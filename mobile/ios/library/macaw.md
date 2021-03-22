# Macaw

## ScaleFit vs Auto Layout

### Avoiding hugging left side of the Macaw View

With Circular Arc Macaw View, for some reason my View sticks to the left more and is not centrally aligned properly. Currently I avoid this situation using a clear background arc to make sure that the Macaw View considers internal margin and for some reason if the Extent of the arc is less than 50% it doesn’t consider the left side of the Arc View.

```swift
// New transparent Arc just to avoid auto layout issue. As the view sticks to close to left hand side.
        let transparentArc = Shape(
            form: Arc(
                ellipse: Ellipse(cx: 0, cy: 0, rx: 160, ry: 160),
                shift: 0.0,
                extent: 5),
            stroke: Stroke(
                fill: Color.clear,
                width: 5,
                cap: .round
        ))
        newNodes.append(transparentArc)
```

