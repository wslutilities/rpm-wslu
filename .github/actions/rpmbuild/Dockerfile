# LA copy of robertdebock/github-action-rpmbuild because taht one don't work
FROM centos:8

WORKDIR /github/workspace
ADD ./compiled_rpms /github/files

RUN dnf install -y make tar gzip rpmdevtools dnf-utils spectool dnf-utils && \
    dnf clean all && \
    rm -r -f /var/cache/*

CMD spectool --get-files --all SPECS/*.spec && \
    yum-builddep --assumeyes SPECS/*.spec && \
    rpmbuild --define '_topdir /github/workspace' -ba SPECS/*.spec && \
    cp SRPMS/* /github/files && \
    cp RPMS/noarch/* /github/files
