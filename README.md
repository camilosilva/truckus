truckus
=======

main composer test

I. Setup of the composer.json when the git packages are present in composer:

https://github.com/composer/composer/issues/1551#issuecomment-12978227

{
    "require": {
        "twig/twig": "1.*",
        "silex/silex": "~1.0",
		"ruckuus/php-activerecord-service-provider": "dev-master"
    },
    "repositories": [
        {
            "type": "git",
            "url": "git://github.com/ruckuus/ActiveRecordServiceProvider.git"
        }
    ]
}


Then run "composer install"

Continue to the next step...


II. To allow fake submodule on composer packages:
http://debuggable.com/posts/git-fake-submodules:4b563ee4-f3cc-4061-967e-0e48cbdd56cb

Meet fake submodules. The idea is simple, instead of using actual submodules, you just trick git into thinking the files belong to the main repository while having the respective sub-dirs remain independent clones. Doing that is simple:

$ cd my-project
$ git clone <subproject-url> my-subproject
$ git add my-subproject/
The important part is the "/" (slash) at the end of the last command. If you omit that, git will automatically assume you want to add 'my-subproject' as a submodule. But if you don't, git just sees the files in the sub-directory and ignores that fact that its a git-repo of its own.


The cool thing is that you can now update a fake sub-module to the latest version as simple as:

$ cd my-subproject
$ git pull
This works because when you are inside my-subproject, git uses the '.git' folder closest to it which is my-subproject/.git. If the sub project is your own, you could even push your changes to it upstream without changing projects.

