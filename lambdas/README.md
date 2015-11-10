## External iterators

Iterator that you have to fully manage yourself.

    for (int i = 0; i < list.size(); ++i) {
        // ...
    }

This is a *familiar*, but not *simple*.
So many things you have to think about:

- the start and end
- the end condition
- the increment

Still an external iterator:

    for (int e : list) {
        // ...
    }

Internal iterator:

    list.forEach(new Consumer<Integer>() {
        public void accept(Integer value) {
            // ...
        }
    }

Thanks to lambdas:

    list.forEach((Integer value) -> System.out.println(value));

Reduced to its simplest form:

    list.forEach(System.out::println);

Notice the distinction:

- `String::valueOf` - reference to static method
- `System.out::println` - reference to instance method

You can use method references when the order of parameters is the same at the left and right sides of the `->` arrow.

Quotes:

- programmers are not anti-social. they are social with the right kinds of people

- a guy who uses *all* the tools is a consultant. I will use only the *right* tools

- lazy evaluations: lambdas + streams leads to: cute code, easier to read, easier to change, efficient

- you are more efficient, not when you work faster, but when you don't work at all

- lazy evaluations is possible only if the functions don't have side effects

- infinite streams cannot exist without laziness, which cannot exist without immutability (no side effects)

Properties of streams:

- sized or not
- ordered
- non-distinct -> `.distinct()`
- non-sorted -> `.sorted()`

An ordered collection means that the elements of the collection have a specific order. The order is independent of the value. A List is an example.

A sorted collection means that not only does the collection have order, but the order depends on the value of the element. A SortedSet is an example.

In contrast, a collection without any order can maintain the elements in any order. A Set is an example.
