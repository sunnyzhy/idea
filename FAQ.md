# FAQ

## 无法创建Scala Class文件
  将Scala的框架添加到项目中，方法是:
1. 在左侧栏中的项目名称上，右键点击Add Framework Support...
2. 在打开的对话框左侧栏中，勾选Scala
3. 点击OK

## Win7系统在删除或移动文件时提示，“操作无法完成，因为其中的文件夹或文件已在另一个程序中打开，请关闭该文件夹或文件，然后重试”
1. 启动任务管理器
2. 选择“性能”标签下的“资源监视器”
3. 在“CPU”标签下的“关联的句柄”栏输入该文件或文件夹的名称
4. 待搜索出结果后逐个结束关联的进程

## Unable to import maven project
```
2019-09-10 15:41:01,677 [ 261511]  ERROR -      #org.jetbrains.idea.maven - com.google.inject.CreationException: Unable to create injector, see the following errors:
 
1) No implementation for org.apache.maven.model.path.PathTranslator was bound.
  while locating org.apache.maven.model.path.PathTranslator
    for field at org.apache.maven.model.interpolation.AbstractStringBasedModelInterpolator.pathTranslator(Unknown Source)
  at org.codehaus.plexus.DefaultPlexusContainer$1.configure(DefaultPlexusContainer.java:350)
 
2) No implementation for org.apache.maven.model.path.UrlNormalizer was bound.
  while locating org.apache.maven.model.path.UrlNormalizer
    for field at org.apache.maven.model.interpolation.AbstractStringBasedModelInterpolator.urlNormalizer(Unknown Source)
  at org.codehaus.plexus.DefaultPlexusContainer$1.configure(DefaultPlexusContainer.java:350)
 
2 errors 
java.lang.RuntimeException: com.google.inject.CreationException: Unable to create injector, see the following errors:
 
1) No implementation for org.apache.maven.model.path.PathTranslator was bound.
  while locating org.apache.maven.model.path.PathTranslator
    for field at org.apache.maven.model.interpolation.AbstractStringBasedModelInterpolator.pathTranslator(Unknown Source)
  at org.codehaus.plexus.DefaultPlexusContainer$1.configure(DefaultPlexusContainer.java:350)
 
2) No implementation for org.apache.maven.model.path.UrlNormalizer was bound.
  while locating org.apache.maven.model.path.UrlNormalizer
    for field at org.apache.maven.model.interpolation.AbstractStringBasedModelInterpolator.urlNormalizer(Unknown Source)
  at org.codehaus.plexus.DefaultPlexusContainer$1.configure(DefaultPlexusContainer.java:350)
 
2 errors
	at com.google.inject.internal.Errors.throwCreationExceptionIfErrorsExist(Errors.java:543)
	at com.google.inject.internal.InternalInjectorCreator.initializeStatically(InternalInjectorCreator.java:159)
	at com.google.inject.internal.InternalInjectorCreator.build(InternalInjectorCreator.java:106)
	at com.google.inject.Guice.createInjector(Guice.java:87)
	at com.google.inject.Guice.createInjector(Guice.java:69)
	at com.google.inject.Guice.createInjector(Guice.java:59)
	at org.codehaus.plexus.DefaultPlexusContainer.addComponent(DefaultPlexusContainer.java:344)
	at org.codehaus.plexus.DefaultPlexusContainer.addComponent(DefaultPlexusContainer.java:332)
	at org.jetbrains.idea.maven.server.Maven3ServerEmbedderImpl.customizeComponents(Maven3ServerEmbedderImpl.java:569)
	at org.jetbrains.idea.maven.server.Maven3ServerEmbedderImpl.customize(Maven3ServerEmbedderImpl.java:540)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at sun.rmi.server.UnicastServerRef.dispatch(UnicastServerRef.java:357)
	at sun.rmi.transport.Transport$1.run(Transport.java:200)
	at sun.rmi.transport.Transport$1.run(Transport.java:197)
	at java.security.AccessController.doPrivileged(Native Method)
	at sun.rmi.transport.Transport.serviceCall(Transport.java:196)
	at sun.rmi.transport.tcp.TCPTransport.handleMessages(TCPTransport.java:573)
	at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run0(TCPTransport.java:834)
	at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.lambda$run$0(TCPTransport.java:688)
	at java.security.AccessController.doPrivileged(Native Method)
	at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run(TCPTransport.java:687)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
	at sun.rmi.transport.StreamRemoteCall.exceptionReceivedFromServer(StreamRemoteCall.java:276)
	at sun.rmi.transport.StreamRemoteCall.executeCall(StreamRemoteCall.java:253)
	at sun.rmi.server.UnicastRef.invoke(UnicastRef.java:162)
	at java.rmi.server.RemoteObjectInvocationHandler.invokeRemoteMethod(RemoteObjectInvocationHandler.java:227)
	at java.rmi.server.RemoteObjectInvocationHandler.invoke(RemoteObjectInvocationHandler.java:179)
	at com.sun.proxy.$Proxy136.customize(Unknown Source)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at com.intellij.execution.rmi.RemoteUtil.invokeRemote(RemoteUtil.java:179)
	at com.intellij.execution.rmi.RemoteUtil.access$300(RemoteUtil.java:39)
	at com.intellij.execution.rmi.RemoteUtil$2$1$1.compute(RemoteUtil.java:160)
	at com.intellij.openapi.util.ClassLoaderUtil.runWithClassLoader(ClassLoaderUtil.java:66)
	at com.intellij.execution.rmi.RemoteUtil.executeWithClassLoader(RemoteUtil.java:231)
	at com.intellij.execution.rmi.RemoteUtil$2$1.invoke(RemoteUtil.java:157)
	at com.sun.proxy.$Proxy136.customize(Unknown Source)
	at org.jetbrains.idea.maven.server.MavenEmbedderWrapper.doCustomize(MavenEmbedderWrapper.java:96)
	at org.jetbrains.idea.maven.server.MavenEmbedderWrapper.lambda$customizeForResolve$1(MavenEmbedderWrapper.java:69)
	at org.jetbrains.idea.maven.server.RemoteObjectWrapper.perform(RemoteObjectWrapper.java:76)
	at org.jetbrains.idea.maven.server.MavenEmbedderWrapper.customizeForResolve(MavenEmbedderWrapper.java:68)
	at org.jetbrains.idea.maven.project.MavenProjectsTree.resolve(MavenProjectsTree.java:1264)
	at org.jetbrains.idea.maven.project.MavenProjectsProcessorResolvingTask.perform(MavenProjectsProcessorResolvingTask.java:44)
	at org.jetbrains.idea.maven.project.MavenProjectsProcessor.doProcessPendingTasks(MavenProjectsProcessor.java:132)
	at org.jetbrains.idea.maven.project.MavenProjectsProcessor.access$000(MavenProjectsProcessor.java:32)
	at org.jetbrains.idea.maven.project.MavenProjectsProcessor$2.run(MavenProjectsProcessor.java:107)
	at org.jetbrains.idea.maven.utils.MavenUtil.lambda$runInBackground$5(MavenUtil.java:449)
	at com.intellij.openapi.application.impl.ApplicationImpl$1.run(ApplicationImpl.java:314)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - IntelliJ IDEA 2018.2.4  Build #IU-182.4505.22 
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - JDK: 1.8.0_152-release 
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - VM: OpenJDK 64-Bit Server VM 
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - Vendor: JetBrains s.r.o 
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - OS: Windows 10 
2019-09-10 15:41:11,284 [ 249118]  ERROR -      #org.jetbrains.idea.maven - Last Action: EditorChooseLookupItem 
```

解决方法：maven版本过高，换一个低版本maven

## 找不到或无法加载主类

原因：由于 target 目录中没有生成对应的 class 文件，导致抛出这一异常

解决方法：

- 方法1: 先 clean 再 Reload project
- 方法2: compile

## 依赖冲突

报如下错误:

```
Caused by: java.lang.NoSuchMethodError
Caused by: java.lang.ClassNotFoundException
Caused by: java.lang.NoClassDefFoundError
```

原因：大概率是由于依赖冲突造成的。

解决方法：

1. 根据抛出的错误信息找出冲突的依赖
2. 修改依赖的版本号，大多数情况需要降低版本号

## IDEA 启动报错 ```https://jb.gg/ide/critical-startup-errors```

```
Resolution
Please try the following steps one by one until the issue is resolved:

In case of "java.nio.file.AccessDeniedException: ...plugins\github-copilot-intellij\copilot-agent\bin\copilot-agent-win.exe", please see this Copilot discussion and the corresponding issue.
If you get "java.net.BindException: Address already in use: bind" exception, please refer to IDEA-238995 for the workaround.
Delete the third-party plug-ins directory (idea.plugins.path in the user's home directory, depends on the OS and IDE version. Please be aware that default locations have changed in 2020.1 release). You can bisect the plug-ins to find the offending one and remove only that plug-in, keeping the working plug-ins.

Note: if the installation is managed by the Toolbox App, plug-ins directory will be located next to the application install location which can be found from the Toolbox properties of the installed app. Look for the directory name starting with the build number and ending with the .plugins, like 192.5728.98.plugins.
Download and install the IDE again, either from the official site or using the Toolbox App. Your settings and projects will be preserved. When installing from .tar.gz on Linux make sure to unpack into the new empty directory, not on the top of the existing installation.
Delete the IDE system (idea.system.path) directory.
In most cases the issue should be already resolved, but if the IDE still doesn't start with the same error dialog, you can also try to backup and delete the configuration directory (idea.config.path).
Contact support with the full exception stacktrace (you can copy/paste it from the error dialog).
```

Examples for IntelliJ IDEA 2022.2:

Windows:

- Configuration (idea.config.path): %APPDATA%\JetBrains\IntelliJIdea2022.2
- Plugins (idea.plugins.path): %APPDATA%\JetBrains\IntelliJIdea2022.2\plugins
- System (idea.system.path): %LOCALAPPDATA%\JetBrains\IntelliJIdea2022.2
- Logs (idea.log.path): %LOCALAPPDATA%\JetBrains\IntelliJIdea2022.2\log

Windows directory:

- **%APPDATA%: C:Users\username\AppData\Roaming***
- **%LOCALAPPDATA%: C:\Users\username\AppData\Local**

macOS:

- Configuration (idea.config.path): ~/Library/Application Support/JetBrains/IntelliJIdea2022.2
- Plugins (idea.plugins.path): ~/Library/Application Support/JetBrains/IntelliJIdea2022.2/plugins
- System (idea.system.path): ~/Library/Caches/JetBrains/IntelliJIdea2022.2
- Logs (idea.log.path): ~/Library/Logs/JetBrains/IntelliJIdea2022.2

Linux:

- Configuration (idea.config.path): ~/.config/JetBrains/IntelliJIdea2022.2
- Plugins (idea.plugins.path): ~/.local/share/JetBrains/IntelliJIdea2022.2
- System (idea.system.path): ~/.cache/JetBrains/IntelliJIdea2022.2
- Logs (idea.log.path): ~/.cache/JetBrains/IntelliJIdea2022.2/log
