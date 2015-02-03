If you override method you may must know ruby allowed to call super method. There are 3 different ways:

1) ```super``` without parentheses — call method with same name and automatic forward arguments
If you change value of variables new value will pass to super method.

```ruby
class A
  def test(t1, t2)
    puts t1
    puts t2
  end
end

class B < A
  def test(t1, t2)
    t1 = 'changed'
    super
  end
end
B.new.test('first', 'second')
```

output is

```
changed
second
```

Ruby don't mind if name of parameters different, it forward by defined order

```ruby
class A
  def test(t1, t2)
    puts t1
    puts t2
  end
end

class B < A
  def test(t2, t1)
    super
  end
end
B.new.test('first', 'second')
```

output is

```
first
second
```

2) ```super()``` with no argument — call super method without any argument
3) ```super(a, b)``` you manual call super method with you order variables