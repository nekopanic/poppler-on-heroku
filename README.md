# poppler-on-heroku

A test app to see if poppler can be installed in a Heroku dyno.

You'll need the right buildpacks:

```
$ heroku buildpacks:clear
$ heroku buildpacks:add https://github.com/mspanc/heroku-buildpack-apt.git
$ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-ruby
```

Make sure `heroku buildpacks` looks like this:

```
$ heroku buildpacks
=== still-cliffs-1195 Buildpack URLs
1. https://github.com/mspanc/heroku-buildpack-apt.git
2. https://github.com/heroku/heroku-buildpack-ruby
```

Then it should build ok. Get onto a dyno with `heroku run bash`

```
$ heroku run bash
Running `bash` attached to terminal... up, run.6533
~ $ wget http://kmmc.in/wp-content/uploads/2014/01/lesson2.pdf
--2015-06-24 21:32:42--  http://kmmc.in/wp-content/uploads/2014/01/lesson2.pdf
Resolving kmmc.in (kmmc.in)... 103.21.59.170
Connecting to kmmc.in (kmmc.in)|103.21.59.170|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1068605 (1.0M) [application/pdf]
Saving to: ‘lesson2.pdf’

100%[===========================================================================================================================================>] 1,068,605    495KB/s   in 2.1s

2015-06-24 21:32:46 (495 KB/s) - ‘lesson2.pdf’ saved [1068605/1068605]

~ $ irb
irb(main):001:0> require 'poppler'
=> true
irb(main):002:0> doc = Poppler::Document.new 'lesson2.pdf'
=> #<Poppler::Document:0x7f407ae851b8 ptr=0x7f407b2c0c40>
irb(main):003:0> doc.pages
=> [#<Poppler::Page:0x7f407aee9870 ptr=0x7f407b2c0c80>, #<Poppler::Page:0x7f407aee97f8 ptr=0x7f407b2c0cc0>, #<Poppler::Page:0x7f407aee97a8 ptr=0x7f407b2c0d00>, #<Poppler::Page:0x7f407aee9758 ptr=0x7f407b2c0d40>, #<Poppler::Page:0x7f407aee96e0 ptr=0x7f407b2c0d80>, #<Poppler::Page:0x7f407aee9640 ptr=0x7f407b2c0dc0>]
```
