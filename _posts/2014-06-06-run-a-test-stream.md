---
layout: post
title: "Run a Test Stream"
---

An issue that has been troubling me for a while is that the 'pspec' parameter in the callback was set to None.

{% highlight python %}
Traceback (most recent call last):
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/common/gstreamer.py", line 55, in verbose_deep_notify_cb
    value = orig.get_property(pspec.name)
AttributeError: 'NoneType' object has no attribute 'name'
{% endhighlight %}

This was due to the change in working of "deep-notify" signal of GObject library. After a lot of research and bug hunting, I figured out that we need to connect the callback to a more specific notification signal. So, I did change in this [commit] and it works as expected.

Now, a simple stream with only the Videotest producer runs perfectly fine. You can take a look at output from [Manager] and [Worker] and a [screenshot] as well. But don't take my word for it, go ahead and run the stream yourself. Here are the steps (for Ubuntu 12.04) to do that:

{% highlight bash %}

# Getting and compiling the latest code

$ sudo add-apt-repository ppa:gstreamer-developers/ppa -y
$ sudo apt-get update -qq
$ sudo apt-get install -qq subversion autopoint python-gst0.10 gstreamer0.10* python-gi python3-gi python-gobject-dev gstreamer1.0* gir1.2-gstreamer-1.0 gir1.2-gst-plugins-base-1.0 libglib2.0-dev gir1.2-glib-2.0 libgirepository1.0-dev libglib2.0-0 gir1.2-gtk-3 libxml-parser-perl python-twisted python-gtk2 python-glade2 python-kiwi pkg-config libglib2.0-dev liborc-0.4-dev bison flex
$ sudo pip install icalendar==2.2 pyparsing python-dateutil
$ wget https://launchpadlibrarian.net/170386464/gst-python1.0_1.2.0.orig.tar.gz
$ tar xvzf gst-python1.0_1.2.0.orig.tar.gz
$ cd gst-python-1.2.0/
$ ./configure
$ make
$ sudo make install
$ cd ..
$ git clone https://github.com/aps-sids/flumotion-orig.git
$ cd flumotion-orig
$ git checkout porting-to-gst1.0
$ ./autogen.sh
$ make

# To run the tests

$ ./run_tests.sh

# Creating the test stream

# in terminal 1
$ ./env bash
$ flumotion-manager -v -T tcp test_config.xml

# in terminal 2
$ ./env bash
$ flumotion-worker -v -T tcp -u user -p test

# in terminal 3 (you need a working flumotion installation for this)
$ flumotion-admin -v

{% endhighlight %}

[commit]: https://github.com/aps-sids/flumotion-orig/commit/29f59d93b0666916374cec0e903f3b0ae4088ac5
[Manager]: http://paste.ubuntu.com/7602897/
[Worker]: http://paste.ubuntu.com/7602905/
[screenshot]: http://a.disquscdn.com/uploads/mediaembed/images/1064/5842/original.jpg
