FROM centos

ADD sources/ /tmp/sources/

RUN yum makecache
RUN yum -y install unzip

RUN cd /tmp/sources/ && unzip ./InstalMgr1.6.2_LNX_X86_64_WAS_8.5.5.zip -d ./ && rm ./InstalMgr1.6.2_LNX_X86_64_WAS_8.5.5.zip
RUN /tmp/sources/installc -acceptLicense
RUN rm -r /tmp/sources/