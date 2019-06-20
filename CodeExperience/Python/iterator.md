# Iterable Iterator

> Every iterator is also an iterable, but not every iterable is an iterator.

> Iterators are objects with a `__next__` method, which will be used when
> the function 'next' is called.

> So if you want to add an iterator behavior to your class, you have to
> add the `__iter__` and the `__next__` method to your class. The `__iter__`
> method returns an iterator object. If the class contains a `__next__`, it
> is enough for the `__iter__` method to return self.

```python
class Reverse:
    
    def __init__(self, data):
        self.data = data
        self.index = len(data)
    
    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopException
        self.index = self.index - 1
        return self.data[self.index]

```