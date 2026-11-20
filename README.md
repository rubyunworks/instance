> **This project is retired.**
>
> Its successor is `Mirror`, part of [Ruby Facets](https://github.com/rubyworks/facets)
> since Facets 4.2.0 (2026-11): `require 'facets/mirror'`, then
> `obj.mirror` in place of `obj.instance`. A mirror gets, sets and lists
> an object's instance variables (`mirror[:name]`, `mirror.to_h`,
> `mirror.update(hash)`) and gives its class and methods. It is not a
> drop-in replacement: the method names differ, and `mirror` doesn't
> clash with Rails' or Singleton's `instance`.
>
> This repository preserves Instance, last released as 0.2.0 in 2014. It
> is no longer maintained.

---

# Instance

## What Is It?

Instance is a *convenient* and *safe* API for accessing and manipulating
an object's state.

## How Does It Work

Instance adds a method to all objects called `#instance`. It returns
an `Instance` delegator that provides the full interface to the
object's state.

Of course, without implementing this in C, directly in the Ruby source,
we  are left to depend on the current provisions Ruby has for accessing
the state of an object. So there are some limitations here. However,
we implement the Ruby code in such a way as to minimize the downsides
by caching all the method definitions the Instance class will utilize.

## Usage

Let's use a very simple example class with which to demonstrate usage.

```ruby
    class Song
      attr_accessor :title
      attr_accessor :artist
      attr_accessor :year

      def initialize(title, artist, year)
        @title  = title
        @artist = artist
        @year   = year
      end
    end
```

Now we can create an instance of Song and work with it's state.

```ruby
    song = Song.new("Paranoid", "Black Sabbath", 1970)

    song.instance.variables
    # => [:@title, :@artist, :@year]

    song.instance.get(:title)
    # => "Paranoid"

    song.instance[:artist]
    # => "Black Sabbath"

    song.instance.to_h        
    # => {:name => "Paranoid", :author => "Black Sabbath", :year => 1970)
```

For a more complete set of usage examples see the [QED](http://rubyworks.github.com/instance/qed.html) documentation.


## Copyrights

Copyright &copy; 2014 [Rubyworks](http://rubyworks.github.io)

BSD-2-Clause License

See [LICENSE.txt](LICENSE.txt) file for license details.

