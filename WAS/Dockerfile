FROM ibmim:base

ADD sources/ /tmp/sources/

RUN cd /tmp/sources/ && unzip WAS_ND_V8.5.5_1_OF_3.zip -d ./ && rm WAS_ND_V8.5.5_1_OF_3.zip
RUN cd /tmp/sources/ && unzip WAS_ND_V8.5.5_2_OF_3.zip -d ./ && rm WAS_ND_V8.5.5_2_OF_3.zip
RUN cd /tmp/sources/ && unzip WAS_ND_V8.5.5_3_OF_3.zip -d ./ && rm WAS_ND_V8.5.5_3_OF_3.zip
RUN /opt/IBM/InstallationManager/eclipse/tools/imcl -input /tmp/sources/WASv85.nd.install.xml -acceptLicense -showProgress

RUN rm -r /tmp/sources/
