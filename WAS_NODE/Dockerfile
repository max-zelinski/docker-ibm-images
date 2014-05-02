FROM was855:base

WORKDIR /opt/IBM/WebSphere/AppServer/
ENTRYPOINT bin/manageprofiles.sh -create -profileName standalone -hostName `(hostname -i)` && \
profiles/standalone/bin/startServer.sh server1 && \
tail -F profiles/standalone/logs/server1/SystemOut.log

EXPOSE 9060 9043 9080 80 9443 5060 5061 443