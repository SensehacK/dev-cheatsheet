# Journey

## Elements Preferences Precedence

So I’ll make this quick

The CSS which is always the first would get first preference for setting the HTML element styles. But we can override it using !important keyword on specific element in CSS selector.

But we may don’t need to even use !important keyword if we add the most important / ranked CSS at the last import, it would automatically get the Last IN imported CSS over the First CSS imports defined.

```typescript
// CSS
import "bootstrap/dist/css/bootstrap.css"; // CSS 1st
import './css/App.css'; // CSS 2nd


 return () {
  <section>
          <Main />
          <Nav />
    </section>
    }

/*
So if CSS 1st has CSS code for <section> tag eg. 'display: block'
and if CSS 2nd has <section> tag eg. 'display: flex'
Then the 2nd CSS would get precedence over the first as it was declared last. So no need to use !important everywhere.
*/
```

