FROM centos:7 


RUN yum install -y yum-plugin-tmprepo
RUN yum install -y spacewalk-repo --tmprepo=https://copr-be.cloud.fedoraproject.org/results/%40spacewalkproject/spacewalk-2.9/epel-7-x86_64/repodata/repomd.xml --nogpg
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm



RUN yum -y install \
        spacewalk-setup-postgresql \
        spacewalk-postgresql \
        supervisor  \
        yum clean all

COPY answerfile.txt /tmp/answerfile.txt

EXPOSE 80 443 5222 68 69

RUN su -c "spacewalk-setup --external-postgresql --answer-file=/tmp/answerfile.txt --skip-db-diskspace-check --skip-db-install" root ; exit 0

ADD supervisord.conf /etc/supervisord.d/supervisord.conf

ENTRYPOINT supervisord -c /etc/supervisord.d/supervisord.conf
