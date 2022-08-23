# BP-Modules

The main conception is systematizing process of creation new repositories.

Here you can find several repositories from which the whole process is build.



## Prerehesitions
You need to :
* Install python 3.9 on your local machine
* Install Allure 2.9.0
* Install docker
* Install docker-compose
* Install make: sudo apt install make

The workflow start from cloning **BP-Init** repository.
## BP-Init
Clone **BP-Init** repository and name it as your new project should be named:
```
git clone git@github.com:Filip-231/BP-Init.git BP-Django-Test 
```


Enter directory what You created:
```
cd BP-Django-Test
```
This repository is made to initialize new projects with several common usefully commands included:

Fill **_PROJECT** with a name of you new project, and **_USER** with the name of your Github user to reset git, specify new project and git user.
```
make git _PROJECT=BP-Django-Test _USER=Filip-231 
```
Now the **BP-Init** repository is transformed to new repository named: abc-test.



## BP-Templates
In this repository all of projects templates are defined including commands and CI/CD process.

You choose between several templates like django / tool / dbt depending on what repository You want to create.

Let's create django rest api:
```
make init LANGUAGE=django
 
```
For technical purposes there is a need to add project name and username to .env file:
```
make set-project-name _PROJECT=BP-Django-Test _USER=Filip-231

```

Commit everything to a new repository (BP-Django-Test) what you just created:
```
make all
```

## BP-Django-Test
This is an example repository created directly from a django template.

Install all necessary packages.
```
make install
```

Don't forget to set up secrets: https://github.com/Filip-231/BP-Test-Django/settings/secrets/actions

To be able to deploy you need to configure the following environment variables:

| **Variable**             | **Description**                                                 | **Example Value**                                                                          |
| ------------------------ |-----------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| DJANGO_SECRET_KEY           | Django secret key consisting multiple characters.               | a7g1no9a2dhcosard72(ale66u5pg4stf9#b97maiccou6sekk                                         |
| TESTING_HOST_IP | Ip address of your linux instance                               | 192.168. 1.1                                                                               |
| TESTING_SSH_PRIVATE_KEY | Privat ssh key which is needed to make ssh tunel.               |       -----BEGIN RSA PRIVATE KEY-----                                                                                     |
| PRODUCTION_HOST_IP | Ip address of your linux instance                               | 192.168. 1.1                                                                               |
| PRODUCTION_SSH_PRIVATE_KEY | Privat ssh key which is needed to make ssh tunel.               |      -----BEGIN RSA PRIVATE KEY-----                                                                                      |

I encourage You to make 2 separate environments for testing and production and pass there specific env vars.  

To configure new environment:
https://github.com/Filip-231/BP-Test-Django/settings/environments/new


In Github You can add a protection rule with reviewer, but the repository need to be visible.

### Features
To see all available commands you can invoke:
``make``
```
Please use make target where target is one of:
all                 commit and push all changes
banner              TITLE= (echo a coloured banner to stdout, designed to demarcate sections)
brew-allure         (install allure with brew long)
build               builds docker image
bump                PART= bump the release version - deduced automatically from commit messages since the last tag unless PART is explicitly provided
changelog           UNRELEASED= update the changelog incrementally. UNRELEASED is the name of the current, as yet unreleased, version)
clean               clean up cache and temp files
clean               clean up temp and trash files
commit              make interactive conventional commit
docker-dev          launch a dev environment inside of a docker container
docs                construct documentations
down-volumes        remove docker images and volumes
format              format code
freeze              generate requirements from setup.cfg
get-version         prints the current version
git                 reset git, specify new project and git user
help                display this help message
init                LANGUAGE=django/tool create cruft project and install pre-requirements
install-allure      ALLURE_VERSION= (install allure)
install             install all requirements
lint                check all code styling
pre-install         install pre-requirements
release             create a new github release
set-project-name    _PROJECT=project _USER=user
tag                 pull tags and tag a new version
test-report         show allure test report
test                ALLURE=True run tests
up                  ALLOWED_HOSTS= SECRET_KEY= turn up the django rest api
update-makefiles    update configuration files
update-project      update cruft project and install pre-requirements # $(_DIR_STRUCTURE)
update              update cruft project and configuration files
venv                install virtual environment
```

All these commands are used to effectively manage the django project.
***
### CI/CD

Complete Github Actions process will automatically occur in your new repository consisting pipelines: 
https://github.com/Filip-231/BP-Test-Django/actions

 
* CI - runs on every push to master and on pull requests
  * test  - run unit and E2E tests 
  * format - checks if code is formatted
  * lint - runs all static code checkers with prospector
  * docker - build and ups docker image
* CD - manually triggered automatic deploys to Oracle cloud environments and GH releases
  * Deploy Testing - need to be successfully deployed testing environment
  * bump_version - bump version of release and push a tag to repo - need to be reviewed to start
  * publish_release - publishing new release in GH releases
  * Deploy Production - after review and approve allowed user, code can be deployed to production
* CI/CD - runs manually, includes CI and CD pipelines connected


## BP-Package 
This repository can install custom package. 
This is example package.