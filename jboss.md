# JBoss

## JBoss CLI commands

version
:whoami
:read-resource

/interface=public:read-attribute(name=resolved-address)


/subsystem=logging/console-handler=CONSOLE:write-attribute(name=filter-spec,value=not(match("HHH000444")))
/subsystem=logging/periodic-rotating-file-handler=FILE:write-attribute(name=filter-spec,value=not(match("HHH000444")))
/subsystem=logging:read-resource

## Wildfly Swarm

https://reference.wildfly-swarm.io/
