# Build

mvn clean package

# RUN

cd docker && docker-compose up -d && docker-compose logs -f 

# ISSUE

In the postBoot script I try to update the log configuration
```
set-log-attributes com.sun.enterprise.server.logging.ODLLogFormatter.ansiColor='false'
```

During server startup following exceptions will be thrown and the parameter will not be updated

```
be_1  | [2021-05-28T07:35:31.356+0000] [] [SEVERE] [] [] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1622187331356] [levelValue: 1000] [[
be_1  |   NCLS-CORE-00002
be_1  | MultiException stack 1 of 3
be_1  | org.glassfish.hk2.api.UnsatisfiedDependencyException: There was no object available for injection at SystemInjecteeImpl(requiredType=LogManagerService,parent=SetLogAttributes,qualifiers={},position=-1,optional=false,self=false,unqualified=null,704894556)
be_1  |         at org.jvnet.hk2.internal.ThreeThirtyResolver.resolve(ThreeThirtyResolver.java:51)
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.resolve(ClazzCreator.java:188)
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.resolveAllDependencies(ClazzCreator.java:211)
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.create(ClazzCreator.java:334)
be_1  |         at org.jvnet.hk2.internal.SystemDescriptor.create(SystemDescriptor.java:463)
be_1  |         at org.jvnet.hk2.internal.PerLookupContext.findOrCreate(PerLookupContext.java:46)
be_1  |         at org.jvnet.hk2.internal.Utilities.createService(Utilities.java:2102)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:759)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:722)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.getService(ServiceLocatorImpl.java:709)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:196)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:180)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.getParameters(CommandExecutorImpl.java:104)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.executeCommand(CommandExecutorImpl.java:177)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.run(CommandExecutorImpl.java:96)
be_1  |         at fish.payara.boot.runtime.BootCommand.execute(BootCommand.java:69)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:136)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:130)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.bootStrap(PayaraMicroImpl.java:1046)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.create(PayaraMicroImpl.java:228)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.main(PayaraMicroImpl.java:215)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
be_1  |         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
be_1  |         at java.lang.reflect.Method.invoke(Method.java:498)
be_1  |         at fish.payara.micro.boot.loader.MainMethodRunner.run(MainMethodRunner.java:50)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:114)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:73)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.create(PayaraMicroLauncher.java:88)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.main(PayaraMicroLauncher.java:72)
be_1  |         at fish.payara.micro.PayaraMicro.main(PayaraMicro.java:456)
be_1  | MultiException stack 2 of 3
be_1  | java.lang.IllegalArgumentException: While attempting to resolve the dependencies of com.sun.enterprise.server.logging.commands.SetLogAttributes errors were found
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.resolveAllDependencies(ClazzCreator.java:224)
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.create(ClazzCreator.java:334)
be_1  |         at org.jvnet.hk2.internal.SystemDescriptor.create(SystemDescriptor.java:463)
be_1  |         at org.jvnet.hk2.internal.PerLookupContext.findOrCreate(PerLookupContext.java:46)
be_1  |         at org.jvnet.hk2.internal.Utilities.createService(Utilities.java:2102)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:759)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:722)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.getService(ServiceLocatorImpl.java:709)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:196)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:180)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.getParameters(CommandExecutorImpl.java:104)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.executeCommand(CommandExecutorImpl.java:177)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.run(CommandExecutorImpl.java:96)
be_1  |         at fish.payara.boot.runtime.BootCommand.execute(BootCommand.java:69)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:136)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:130)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.bootStrap(PayaraMicroImpl.java:1046)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.create(PayaraMicroImpl.java:228)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.main(PayaraMicroImpl.java:215)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
be_1  |         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
be_1  |         at java.lang.reflect.Method.invoke(Method.java:498)
be_1  |         at fish.payara.micro.boot.loader.MainMethodRunner.run(MainMethodRunner.java:50)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:114)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:73)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.create(PayaraMicroLauncher.java:88)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.main(PayaraMicroLauncher.java:72)
be_1  |         at fish.payara.micro.PayaraMicro.main(PayaraMicro.java:456)
be_1  | MultiException stack 3 of 3
be_1  | java.lang.IllegalStateException: Unable to perform operation: resolve on com.sun.enterprise.server.logging.commands.SetLogAttributes
be_1  |         at org.jvnet.hk2.internal.ClazzCreator.create(ClazzCreator.java:363)
be_1  |         at org.jvnet.hk2.internal.SystemDescriptor.create(SystemDescriptor.java:463)
be_1  |         at org.jvnet.hk2.internal.PerLookupContext.findOrCreate(PerLookupContext.java:46)
be_1  |         at org.jvnet.hk2.internal.Utilities.createService(Utilities.java:2102)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:759)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.internalGetService(ServiceLocatorImpl.java:722)
be_1  |         at org.jvnet.hk2.internal.ServiceLocatorImpl.getService(ServiceLocatorImpl.java:709)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:196)
be_1  |         at com.sun.enterprise.v3.admin.CommandRunnerImpl.getModel(CommandRunnerImpl.java:180)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.getParameters(CommandExecutorImpl.java:104)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.executeCommand(CommandExecutorImpl.java:177)
be_1  |         at com.sun.enterprise.admin.cli.embeddable.CommandExecutorImpl.run(CommandExecutorImpl.java:96)
be_1  |         at fish.payara.boot.runtime.BootCommand.execute(BootCommand.java:69)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:136)
be_1  |         at fish.payara.boot.runtime.BootCommands.executeCommands(BootCommands.java:130)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.bootStrap(PayaraMicroImpl.java:1046)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.create(PayaraMicroImpl.java:228)
be_1  |         at fish.payara.micro.impl.PayaraMicroImpl.main(PayaraMicroImpl.java:215)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
be_1  |         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
be_1  |         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
be_1  |         at java.lang.reflect.Method.invoke(Method.java:498)
be_1  |         at fish.payara.micro.boot.loader.MainMethodRunner.run(MainMethodRunner.java:50)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:114)
be_1  |         at fish.payara.micro.boot.loader.Launcher.launch(Launcher.java:73)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.create(PayaraMicroLauncher.java:88)
be_1  |         at fish.payara.micro.boot.PayaraMicroLauncher.main(PayaraMicroLauncher.java:72)
be_1  |         at fish.payara.micro.PayaraMicro.main(PayaraMicro.java:456)
be_1  | ]]

```