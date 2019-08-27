<p align="center"><img src="../assets/img/logo.svg" alt="logo"></p>
<br>
<p align="center"><img src="../assets/img/Symfony4Dicker_title.svg" alt="title"></p>

# User Guide

## Content




### Varnish Symfony Integration

~~~~
composer require \
    lcobucci/jwt \
    lexik/jwt-authentication-bundle \
    symfony-bundles/redis-bundle \
    symfony/cache \
    symfony/lts \
    symfony/templating

composer require symfony/dotenv --dev
~~~~

Change /bin/console file

Add to src/Kernel.php:

----


    public function getCacheDir()
    {
        return $this->getProjectDir().'/var/cache/'.$this->environment;
    }
    
    public function getLogDir()
    {
        return $this->getProjectDir().'/var/log';
    }
----



