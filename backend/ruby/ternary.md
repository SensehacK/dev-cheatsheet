# Ternary



## Code


```rb
if apple_stock > 1
  :eat_apple
else
  :buy_apple
end

```

Can be converted to 

```rb
apple_stock > 1 ? :eat_apple : :buy_apple
```

[Source](https://www.rubyguides.com/2019/10/ruby-ternary-operator/)


## Default nil case

Nil coalescing stuff in ruby for giving a default value.

```rb
x = value || "default_if_value_is_nil_or_false"
x = nil_value || "default"
```

[SO](https://stackoverflow.com/questions/14095004/value-or-default)


[doc](https://www.rubyguides.com/2018/01/ruby-nil/)