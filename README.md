# Centos dev with mock

# Purpose

Scratch repo for playing around with centos, mock and nexus


# To run

To Run mock

bring up nexus:

    docker-compose up -d  
    docker-compose logs -f nexus

start docker container:

    docker run --cap-add=SYS_ADMIN ...  # note this is handled by docker-compose

    docker-compose build  centos-dev
    docker-compose run --rm centos-dev

build in mock:

    mock --configdir /mock/config --resultdir /mock/out --rebuild curl-7.29.0-54.el7.src.rpm
    mock --configdir /mock/config --resultdir /mock/out --rebuild less-458-9.el7.src.rpm

    if [[ ! -z "$JENKINS_URL" ]]; then
    mock --configdir /mock/config --orphanskill
    mock --configdir /mock/config --scrub=all
    fi


## Interesting directories

/etc/mock
/var/lib/mock/
/var/cache/mock/


## References

Mock:
https://github.com/rpm-software-management/mock/wiki
https://github.com/rpm-software-management/mock/wiki/FAQ
https://linux.die.net/man/1/mock
https://github.com/rpm-software-management/mock/wiki#mock-inside-docker
https://fedoraproject.org/wiki/Using_Mock_to_test_package_builds
http://miroslav.suchy.cz/blog/archives/2015/05/28/increase_mock_performance_-_build_packages_in_memory/index.html

Mirrors:
https://wiki.centos.org/AdditionalResources/Repositories
http://mirror.centos.org/centos/
http://mirror.centos.org/altarch/
http://vault.centos.org/ # source rpms
https://dl.fedoraproject.org/pub/epel/
https://wiki.centos.org/AdditionalResources/Repositories/GoogleYumRepos
https://packages.microsoft.com/yumrepos/vscode/

Nexus:
https://hub.docker.com/r/sonatype/nexus3/
https://help.sonatype.com/repomanager3/configuration/repository-management
https://help.sonatype.com/repomanager3/formats/yum-repositories
https://blog.sonatype.com/staging-in-nexus-repository-3.11
