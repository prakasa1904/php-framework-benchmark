# PHP Framework Benchmark

This project attempts to mesure minimum overhead (minimum bootstrap cost) of PHP frameworks in real world.

So I think the minimun applications to benchmark should not include:

* cost of template engine (HTML output)
* cost of database manipulation
* cost of debugging information

Components like Template engine or ORM/Database library are out of scope in this project.

## Benchmarking Policy

This is `optimize` branch.

This branch accepts optimization like:

* removing components/configurations which are not used
* optimized configuration

Caution: Not all the frameworks are optimized!

If you are interested in benchmarking with no optimization/manipulation (removing components/configurations which are not used), See [master](https://github.com/kenjis/php-framework-benchmark/) branch.

If you find something wrong with my code, please feel free to send Pull Requests. But please note optimizing only for "Hello World" is not acceptable. Building fastest "Hello World" application is not the goal in this project.

## Frameworks to Benchmark

* Phalcon 2.0.0-RC1
* Ice 1.0.10
* Slim 2.6.2
* CodeIgniter 3.0.0
* Lumen 5.0.8
* Yii 2.0.4
* Silex 1.2.4
* Cygnite 1.3.1
* BEAR.Sunday 1.0.0-rc.3
* FuelPHP 1.8-dev
* CakePHP 3.0.2
* Aura 2.0.2
* Symfony 2.6.6
* Laravel 5.0.27
* Zend Framework 2.4.0
* TYPO3 Flow 2.3.3

## Results

### Benchmarking Environment

* CentOS 6.5 64bit (VM; VirtualBox)
  * PHP 5.5.23 (Remi RPM)
    * Zend OPcache v7.0.4-dev
  * Apache 2.2

### Hello World Benchmark

These are my benchmarks, not yours. **I encourage you to run on your environments.**

(2015/05/02)

|framework          |requests per second|relative|peak memory|relative|
|-------------------|------------------:|-------:|----------:|-------:|
|phalcon-2.0        |           1,427.29|    34.8|       0.50|     1.0|
|ice-1.0            |           1,080.03|    26.4|       0.50|     1.0|
|slim-2.6           |             775.52|    18.9|       0.50|     1.0|
|codeigniter-3.0    |             704.02|    17.2|       0.50|     1.0|
|lumen-5.0          |             371.62|     9.1|       1.00|     2.0|
|yii-2.0            |             353.19|     8.6|       1.75|     3.5|
|silex-1.2          |             348.75|     8.5|       1.00|     2.0|
|cygnite-1.3        |             340.16|     8.3|       0.75|     1.5|
|bear-1.0           |             328.33|     8.0|       1.00|     2.0|
|fuel-1.8-dev       |             299.56|     7.3|       0.75|     1.5|
|cake-3.0       (*) |             345.06|     8.4|       1.00|     2.0|
|aura-2.0           |             208.22|     5.1|       1.00|     2.0|
|symfony-2.6    (*) |             181.19|     4.4|       2.00|     4.0|
|laravel-5.0        |              71.75|     1.8|       2.75|     5.5|
|zf-2.4         (*) |              75.24|     1.8|       3.00|     6.0|
|typo3-flow-2.3     |              40.96|     1.0|       5.25|    10.5|

Note(1): All the results are run on php with `phalcon.so` and `ice.so`. If you don't load phalcon.so or ice.so, the rps except for Phalcon or Ice probably increase a bit.

Note(2): Only frameworks with (*) mark are optimized, and optimized does not mean fully optimized. Other frameworks are not optimized at all.

#### Comparision before and after optimization

@TODO

## How to Benchmark

Install source code as <http://localhost/php-framework-benchmark/>.

~~~
$ git clone https://github.com/kenjis/php-framework-benchmark.git
$ cd php-framework-benchmark
$ git checkout optimize
$ sh setup.sh
~~~

Run benchmarks.

~~~
$ sh benchmark.sh
~~~

See <http://localhost/php-framework-benchmark/>.

## Linux Kernel Configuration

I added below in `/etc/sysctl.conf`

~~~
# Added
net.netfilter.nf_conntrack_max = 100000
net.nf_conntrack_max = 100000
net.ipv4.tcp_max_tw_buckets = 180000
net.ipv4.tcp_tw_recycle = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_fin_timeout = 10
~~~

and run `sudo sysctl -p`.

If you want to see current configuration, run `sudo sysctl -a`.

## Reference

* [Phalcon](http://phalconphp.com/)
* [Ice](http://www.iceframework.org/)
* [Slim](http://www.slimframework.com/)
* [CodeIgniter](http://www.codeigniter.com/)
* [Lumen](http://lumen.laravel.com/)
* [Yii](http://www.yiiframework.com/)
* [Silex](http://silex.sensiolabs.org/)
* [Cygnite](http://www.cygniteframework.com/)
* [BEAR.Sunday](https://bearsunday.github.io/)
* [FuelPHP](http://fuelphp.com/)
* [CakePHP](http://cakephp.org/)
* [Aura](http://auraphp.com/)
* [Symfony](http://symfony.com/)
  * [How to Deploy a Symfony Application](http://symfony.com/doc/current/cookbook/deployment/tools.html)
* [Laravel](http://laravel.com/)
* [Zend Framework](http://framework.zend.com/)
* [TYPO3 Flow](http://flow.typo3.org/)

## Related

* [PHP ORM Benchmark](https://github.com/kenjis/php-orm-benchmark)
* [PHP User Agent Parser Benchmarks](https://github.com/kenjis/user-agent-parser-benchmarks)
