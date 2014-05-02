FROM ibmim:base

ADD sources/ /tmp/sources/

RUN yum makecache
RUN yum -y install ksh

RUN groupadd ihs
RUN useradd -g ihs ihs

RUN cd /tmp/sources/ && unzip WAS_V8.5.5_SUPPL_1_OF_3.zip -d ./ && rm WAS_V8.5.5_SUPPL_1_OF_3.zip
RUN cd /tmp/sources/ && unzip WAS_V8.5.5_SUPPL_2_OF_3.zip -d ./ && rm WAS_V8.5.5_SUPPL_2_OF_3.zip
RUN cd /tmp/sources/ && unzip WAS_V8.5.5_SUPPL_3_OF_3.zip -d ./ && rm WAS_V8.5.5_SUPPL_3_OF_3.zip
RUN /opt/IBM/InstallationManager/eclipse/tools/imcl -input /tmp/sources/WASv85.ihs.install.xml -acceptLicense -showProgress
RUN rm -r /tmp/sources/

RUN /opt/IBM/HTTPServer/bin/htpasswd -cmb /opt/IBM/HTTPServer/conf/admin.passwd ihsadmin 1

RUN cp -r /opt/IBM/WebSphere/Plugins/config/templates /opt/IBM/WebSphere/Plugins/config/webserver1 
RUN /opt/IBM/WebSphere/Plugins/bin/ConfigureIHSPlugin.sh -plugin.home /opt/IBM/WebSphere/Plugins/ -plugin.config.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml -ihs.conf.file /opt/IBM/HTTPServer/conf/httpd.conf -ihs.admin.usergroup ihs -operating.system Linux -operating.system.arch 64 -WAS.webserver.name webserver1

RUN chown -R ihs:ihs /opt/IBM/HTTPServer/
RUN chown -R ihs:ihs /opt/IBM/WebSphere/Plugins/

RUN sed -i -e "s/@@AdminPort@@/8008/g" /opt/IBM/HTTPServer/conf/admin.conf
RUN sed -i -e "s/@@SetupadmUser@@/ihs/g" /opt/IBM/HTTPServer/conf/admin.conf
RUN sed -i -e "s/@@SetupadmGroup@@/ihs/g" /opt/IBM/HTTPServer/conf/admin.conf

WORKDIR /opt/IBM/HTTPServer
CMD bin/adminctl start && touch logs/access_log && tail -F logs/access_log

EXPOSE 80 8008