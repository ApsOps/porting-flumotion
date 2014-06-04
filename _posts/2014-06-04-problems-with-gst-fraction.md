---
layout: post
title: "Problems with Gst.Fraction"
---

There is a Fraction class I need to port but I'm facing a few problems.

In gst-0.10, we use it like `gst.Fraction(2,4)` and we get a `<gst.Fraction 1/2>` Here's the details of gst.Fraction :

{% highlight python %}
Type:            classobj
String form:     gst.Fraction
File:            /usr/lib/python2.7/dist-packages/gst-0.10/gst/__init__.py
Init definition: gst.Fraction(self, num, denom=1)
Source:
class Fraction(Value):
    def __init__(self, num, denom=1):
        def __gcd(a,b):
            while b != 0:
                tmp = a
                a = b
                b = tmp % b
            return abs(a)

        def __simplify():
            num = self.num
            denom = self.denom
    
            if num < 0:
                num = -num
                denom = -denom
    
            # Compute greatest common divisor
            gcd = __gcd(num,denom)
            if gcd != 0:
              num /= gcd
              denom /= gcd
    
            self.num = num
            self.denom = denom

        Value.__init__(self, 'fraction')
    
        self.num = num
        self.denom = denom

        __simplify()

    def __repr__(self):
        return '<gst.Fraction %d/%d>' % (self.num, self.denom)

    def __eq__(self, other):
        if isinstance(other, Fraction):
            return self.num * other.denom == other.num * self.denom
        return False

    def __ne__(self, other):
        return not self.__eq__(other)

    def __mul__(self, other):
        if isinstance(other, Fraction):
            return Fraction(self.num * other.num,
                            self.denom * other.denom)
        elif isinstance(other, int):
            return Fraction(self.num * other, self.denom)
        raise TypeError

    __rmul__ = __mul__

    def __div__(self, other):
        if isinstance(other, Fraction):
            return Fraction(self.num * other.denom,
                            self.denom * other.num)
        elif isinstance(other, int):
            return Fraction(self.num, self.denom * other)
        return TypeError

    def __rdiv__(self, other):
        if isinstance(other, int):
            return Fraction(self.denom * other, self.num)
        return TypeError

    def __float__(self):
        return float(self.num) / float(self.denom)

{% endhighlight %}

Now, gi has some overrides to achieve this functionality. But, this is not available in Gstreamer-1.2.1 (latest version available in Ubuntu 12.04). So, I tried implementing it in this [commit]. It failed with this error:

{% highlight python %}
Traceback (most recent call last):
  File "/home/aps/workspace/gsoc/flumotion-orig/bin/flumotion-manager", line 41, in <module>
    from flumotion.common import boot
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/__init__.py", line 35, in <module>
    class Fraction(Gst.Fraction):
  File "/usr/lib/python2.7/dist-packages/gi/types.py", line 212, in __init__
    super(GObjectMeta, cls).__init__(name, bases, dict_)
  File "/usr/lib/python2.7/dist-packages/gi/_gobject/__init__.py", line 65, in __init__
    cls._type_register(cls.__dict__)
  File "/usr/lib/python2.7/dist-packages/gi/_gobject/__init__.py", line 119, in _type_register
    type_register(cls, namespace.get('__gtype_name__'))
TypeError: Error when calling the metaclass bases
    argument must be a GObject subclass
{% endhighlight %}

But, running    `Gst.Fraction.__class__`      in python shell gives output   `gi.types.GObjectMeta`

Placing the [Gst.py] file inside /usr/lib/python27/dist-packages/gi/overrides/ fixes the problem but it's not a good/valid fix.

The only (hackish) way I could think of is writing a function that gives same results (if possible) as Gst.Fraction. If you can think of any idea, please let me know in comments. Thanks!

[commit]: https://github.com/aps-sids/flumotion-orig/commit/da4e2cb84f4b883158c4fb17c5b31eecc2b745a6
[Gst.py]: http://cgit.freedesktop.org/gstreamer/gst-python/tree/gi/overrides/Gst.py
