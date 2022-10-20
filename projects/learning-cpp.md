# Handmade Hero Course

tags: #c #cpp #gamedev

[HMH Playlist](https://www.youtube.com/playlist?list=PLnuhp3Xd9PYTt6svyQPyRO_AAuMWGxPzU)
[C++ Playlist](https://www.youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb)

-------------------

**[HMH - Day 13](https://www.youtube.com/watch?v=Lt9DfMzZ9sI)**

I dont know if I got this correctly, but the purpose of `union` is to transpose
the memory of something into different data type 

So doing something like:

```cpp
union sth {
    bool BooleanValue;
    char CharValue;
} sth;
```

I could technically do `sth.BooleanValue` or `sth.CharValue` and get the same
memory location but marshalled for the corresponding type.

What happens if they are different sizes?

Apparently the size of the union becomes the size of the largest member, every
member address is the same so I guess you would see in memery as:

```cpp
union sth {
    uint32 SmallBitValue;
    uint64 BigBitValue;
} sth;

//             B1 -- -- -- B2 -- -- -- B3 -- -- -- B4 -- -- --
//Address: FF  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
//
//             SmallBitValue- -- -- --
//             BigBitValue -- -- -- -- -- -- -- -- -- -- -- --
//
// The size is halfed but for the sake of the illustration (～￣▽￣)～)
```

[Source 6.7.2.1/16](https://www.open-std.org/JTC1/SC22/WG14/www/docs/n2310.pdf)

-------------------

## Learning resources

### Youtube channels

- [CppCast](https://www.youtube.com/channel/UCuCjADS4u3uJDTqUaG0H9dA)
- [CppCon](https://www.youtube.com/user/CppCon)
