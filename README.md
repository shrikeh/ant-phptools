ant-phptools
================

A Composer-friendly port of the PEAR-based Template for Jenkins Jobs for PHP Projects (http://jenkins-php.org)

## Theory of operation

While the Jenkins Jobs relies on PEAR, this port relies on the new hotness that is Composer (http://getcomposer.org/).
While PEAR is a system-level library container, Composer is an application-level dependency manager, which allows more granularity of control over which libraries and version are required for use.
To get around the need for granular controls for testing, a Jenkins admin would have to install ALL the dependencies system-wide to meet any variety of testing criteria (TDD, BDD, SpecBDD, etc).

This library gets around this by keeping in sync with the application composer dependencies. It has hooks for:

* PHPUnit (https://github.com/sebastianbergmann/phpunit)
* Behat (http://behat.org/)
* PHPSpec2 (http://phpspec.net/)
* phpmd (PHP Mess Detector - http://phpmd.org/)
* phpcb (PHP Code Browser - https://github.com/Mayflower/PHP_CodeBrowser)
* phpcpd (PHP Copy Paste Detector - https://github.com/sebastianbergmann/phpcpd)
* phploc (PHP Lines of Code - https://github.com/sebastianbergmann/phploc)
* phpcs (PHP_CodeSniffer - https://github.com/squizlabs/PHP_CodeSniffer)
* pdepend (PHP_Depend - http://pdepend.org/)


## Usage

Clone or download this repo into a location readable by ant:

```shell
git clone https://github.com/shrikeh/ant-phptools.git
```

Then, in your ant `build.xml` file, reference the `tests.xml` file by `<include>` (not `<import>`):

```xml
<include file="${basedir}/ant-phptools/tests.xml"/>
```

To use the tests, you can then simply add a reference to the tests within, such as:
```xml
<target name="test" depends="prepare, phptools.phptests-parallel" />
```

For every existing hook, the tools will check to see if the corresponding phar is available, and if so, it will assume the target is to be run. Thus, by adding or subtracting from your require-dev section of the `composer.json` file, your ant file will automatically run the new automated testing referenced.


## Further configuration
By default, the `tests.xml` uses sensible Symfony-style defaults for paths. However, ALL of the variables it uses are variables, allowing as much configuration as you wish.

There are several ways to configure the include:

* If you do not wish to use the default `php-build-tools.properties` file, copy the file, alter the values you wish, and simply set the `${phptools.properties}` to the path of the new file:

```xml
<property name="${phptools.properties}" location="phptools.properties.local" />
```
* Alternatively, you can set individual values. Because ant works on the theory that variables already configured are read only, you can set variables prior to running the `tests-parallel` target and all will be well.



