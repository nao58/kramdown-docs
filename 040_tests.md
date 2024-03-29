Tests and Benchmark
===================

Tests
-----

There exist several test suites for testing the correctness of a Markdown implementation. The original [Markdown Test Suite](http://daringfireball.net/projects/downloads/MarkdownTest_1.0.zip) is the standard which one needs to test against. The [PHP Markdown suite](http://www.michelf.com/docs/projets/mdtest-1.0.zip) contains the original test suite and several more tests (some specifically geared towards the extension of the PHP Markdown Extra package). I have used the latter test tool to roughly verify that kramdown is able to parse standard Markdown. However, since the syntax used by kramdown varies slightly from standard Markdown most of the tests fail - which is fine. When looking at the differences one can see that the failures result from these differences.

Besides using the above mentioned test suite kramdown comes with its own set of tests which is used to verify that the implementation matches the kramdown specification.

If you believe you have found a bug in the implementation, please follow these steps:

* Check the [syntax page][kramdown Syntax] and see if the behaviour is not intended.
* If the behaviour is not intended and it seems that kramdown should parse some text in another fashion, please open a [bug report](https://github.com/gettalong/kramdown/issues) and attach two files: one with the text and one with the HTML conversion you think is correct.

Benchmark
---------

kramdown comes with a small benchmark to test how fast it is in regard to four other Ruby Markdown implementations: Maruku, BlueFeather, BlueCloth, RDiscount and Redcarpet. The first two are written using only Ruby, the latter three are written in C and need to be compiled.

As one can see below, kramdown is currently (January 2014) ~2.5x faster than Maruku, ~4-6x faster than BlueFeather but ~30x slower than BlueCloth and RDiscount and ~150x slower than Redcarpet:

~~~
Running tests on 2014-01-05 under ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-linux]

Test using file mdsyntax.text and 20 runs
Rehearsal ----------------------------------------------------
kramdown 1.3.0     1.090000   0.020000   1.110000 (  1.102094)
Maruku 0.7.0       3.140000   0.010000   3.150000 (  3.151116)
BlueFeather 0.41   5.140000   0.000000   5.140000 (  5.136591)
BlueCloth 2.2.0    0.050000   0.000000   0.050000 (  0.057502)
RDiscount 2.0.7    0.020000   0.000000   0.020000 (  0.015115)
redcarpet 3.0.0    0.000000   0.000000   0.000000 (  0.004641)
------------------------------------------- total: 9.470000sec

                       user     system      total        real
kramdown 1.3.0     1.200000   0.000000   1.200000 (  1.199684)
Maruku 0.7.0       3.010000   0.040000   3.050000 (  3.043411)
BlueFeather 0.41   5.720000   0.000000   5.720000 (  5.723845)
BlueCloth 2.2.0    0.040000   0.000000   0.040000 (  0.040749)
RDiscount 2.0.7    0.020000   0.000000   0.020000 (  0.017600)
redcarpet 3.0.0    0.000000   0.000000   0.000000 (  0.004822)

Real time of X divided by real time of kramdown
Maruku             2.5368
BlueFeather        4.7711
BlueCloth          0.034
RDiscount          0.0147
redcarpet          0.004

Test using file mdbasics.text and 20 runs
Rehearsal ----------------------------------------------------
kramdown 1.3.0     0.220000   0.000000   0.220000 (  0.217277)
Maruku 0.7.0       0.850000   0.000000   0.850000 (  0.847144)
BlueFeather 0.41   1.290000   0.010000   1.300000 (  1.291695)
BlueCloth 2.2.0    0.010000   0.000000   0.010000 (  0.012484)
RDiscount 2.0.7    0.000000   0.000000   0.000000 (  0.004158)
redcarpet 3.0.0    0.000000   0.000000   0.000000 (  0.001721)
------------------------------------------- total: 2.380000sec

                       user     system      total        real
kramdown 1.3.0     0.210000   0.000000   0.210000 (  0.215760)
Maruku 0.7.0       0.590000   0.000000   0.590000 (  0.591681)
BlueFeather 0.41   1.360000   0.000000   1.360000 (  1.362281)
BlueCloth 2.2.0    0.010000   0.000000   0.010000 (  0.013973)
RDiscount 2.0.7    0.010000   0.000000   0.010000 (  0.005797)
redcarpet 3.0.0    0.000000   0.000000   0.000000 (  0.001692)

Real time of X divided by real time of kramdown
Maruku             2.7423
BlueFeather        6.3139
BlueCloth          0.0648
RDiscount          0.0269
redcarpet          0.0078
~~~

And here are some graphs which show the execution times of the various kramdown releases on different Ruby interpreters:

![Execution Time Performance for ruby 1.8.7p302](http://kramdown.gettalong.org/img/graph-ruby-1.8.7-302.png)!

![Execution Time Performance for ruby 1.9.2p320](http://kramdown.gettalong.org/img/graph-ruby-1.9.2p320-320.png)!

![Execution Time Performance for ruby 1.9.3p448](http://kramdown.gettalong.org/img/graph-ruby-1.9.3p448-448.png)!

![Execution Time Performance for ruby 2.0.0p247](http://kramdown.gettalong.org/img/graph-ruby-2.0.0p247-247.png)!

![Execution Time Performance for ruby 2.1.0p0](http://kramdown.gettalong.org/img/graph-ruby-2.1.0p0-0.png)!

![Execution Time Performance for jruby 1.7.3](http://kramdown.gettalong.org/img/graph-jruby-1.7.3-385.png)!

![Execution Time Performance for rubinius 2.0.0](http://kramdown.gettalong.org/img/graph-rubinius-2.0.0-0.png)!
