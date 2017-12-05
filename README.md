# gradle-include-build-zip
Project to reproduce failing composite build:
* Project in `zip-producing-project` creates a zip, and configures publishing using the `maven-publish` plugin.
* Project in `zip-consuming-project` tries to unzip that artifact using a composite-build.

To reproduce, go to zip-consuming-project and run `./gradlew unzip -is`:

```
Selected primary task 'unzip' from project :
Found project 'project :zip-producing-project' as substitute for module 'test:zip-producing-project'.

FAILURE: Build failed with an exception.

* Where:
Build file 'C:\work\gradle-include-build-zip\zip-consuming-project\build.gradle' line: 18

* What went wrong:
Could not determine the dependencies of task ':unzip'.
> Could not resolve all files for configuration ':dummy'.
   > Could not find zip-producing-project.zip (project :zip-producing-project).

* Try:
Run with --debug option to get more log output.

* Exception is:
org.gradle.api.internal.tasks.TaskDependencyResolveException: Could not determine the dependencies of task ':unzip'.
        at org.gradle.api.internal.tasks.CachingTaskDependencyResolveContext.resolve(CachingTaskDependencyResolveContext.java:68)
        at org.gradle.api.internal.tasks.CachingTaskDependencyResolveContext.getDependencies(CachingTaskDependencyResolveContext.java:56)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionPlan.addToTaskGraph(DefaultTaskExecutionPlan.java:176)
        at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter.addTasks(DefaultTaskGraphExecuter.java:111)
        at org.gradle.execution.TaskNameResolvingBuildConfigurationAction.configure(TaskNameResolvingBuildConfigurationAction.java:47)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.configure(DefaultBuildConfigurationActionExecuter.java:48)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.access$000(DefaultBuildConfigurationActionExecuter.java:25)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter$1.proceed(DefaultBuildConfigurationActionExecuter.java:54)
        at org.gradle.execution.DefaultTasksBuildExecutionAction.configure(DefaultTasksBuildExecutionAction.java:44)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.configure(DefaultBuildConfigurationActionExecuter.java:48)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.access$000(DefaultBuildConfigurationActionExecuter.java:25)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter$1.proceed(DefaultBuildConfigurationActionExecuter.java:54)
        at org.gradle.execution.ExcludedTaskFilteringBuildConfigurationAction.configure(ExcludedTaskFilteringBuildConfigurationAction.java:47)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.configure(DefaultBuildConfigurationActionExecuter.java:48)
        at org.gradle.execution.DefaultBuildConfigurationActionExecuter.select(DefaultBuildConfigurationActionExecuter.java:36)
        at org.gradle.initialization.DefaultGradleLauncher$CalculateTaskGraph.run(DefaultGradleLauncher.java:268)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:336)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:328)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.execute(DefaultBuildOperationExecutor.java:199)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:110)
        at org.gradle.initialization.DefaultGradleLauncher.constructTaskGraph(DefaultGradleLauncher.java:175)
        at org.gradle.initialization.DefaultGradleLauncher.doBuildStages(DefaultGradleLauncher.java:130)
        at org.gradle.initialization.DefaultGradleLauncher.executeTasks(DefaultGradleLauncher.java:109)
        at org.gradle.internal.invocation.GradleBuildController$1.call(GradleBuildController.java:78)
        at org.gradle.internal.invocation.GradleBuildController$1.call(GradleBuildController.java:75)
        at org.gradle.internal.work.DefaultWorkerLeaseService.withLocks(DefaultWorkerLeaseService.java:152)
        at org.gradle.internal.invocation.GradleBuildController.doBuild(GradleBuildController.java:100)
        at org.gradle.internal.invocation.GradleBuildController.run(GradleBuildController.java:75)
        at org.gradle.tooling.internal.provider.ExecuteBuildActionRunner.run(ExecuteBuildActionRunner.java:28)
        at org.gradle.launcher.exec.ChainingBuildActionRunner.run(ChainingBuildActionRunner.java:35)
        at org.gradle.tooling.internal.provider.ValidatingBuildActionRunner.run(ValidatingBuildActionRunner.java:32)
        at org.gradle.launcher.exec.RunAsBuildOperationBuildActionRunner$1.run(RunAsBuildOperationBuildActionRunner.java:43)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:336)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:328)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.execute(DefaultBuildOperationExecutor.java:199)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:110)
        at org.gradle.launcher.exec.RunAsBuildOperationBuildActionRunner.run(RunAsBuildOperationBuildActionRunner.java:40)
        at org.gradle.tooling.internal.provider.SubscribableBuildActionRunner.run(SubscribableBuildActionRunner.java:51)
        at org.gradle.launcher.exec.InProcessBuildActionExecuter.execute(InProcessBuildActionExecuter.java:47)
        at org.gradle.launcher.exec.InProcessBuildActionExecuter.execute(InProcessBuildActionExecuter.java:30)
        at org.gradle.launcher.exec.BuildTreeScopeBuildActionExecuter.execute(BuildTreeScopeBuildActionExecuter.java:39)
        at org.gradle.launcher.exec.BuildTreeScopeBuildActionExecuter.execute(BuildTreeScopeBuildActionExecuter.java:25)
        at org.gradle.tooling.internal.provider.ContinuousBuildActionExecuter.execute(ContinuousBuildActionExecuter.java:80)
        at org.gradle.tooling.internal.provider.ContinuousBuildActionExecuter.execute(ContinuousBuildActionExecuter.java:53)
        at org.gradle.tooling.internal.provider.ServicesSetupBuildActionExecuter.execute(ServicesSetupBuildActionExecuter.java:57)
        at org.gradle.tooling.internal.provider.ServicesSetupBuildActionExecuter.execute(ServicesSetupBuildActionExecuter.java:32)
        at org.gradle.tooling.internal.provider.GradleThreadBuildActionExecuter.execute(GradleThreadBuildActionExecuter.java:36)
        at org.gradle.tooling.internal.provider.GradleThreadBuildActionExecuter.execute(GradleThreadBuildActionExecuter.java:25)
        at org.gradle.tooling.internal.provider.ParallelismConfigurationBuildActionExecuter.execute(ParallelismConfigurationBuildActionExecuter.java:43)
        at org.gradle.tooling.internal.provider.ParallelismConfigurationBuildActionExecuter.execute(ParallelismConfigurationBuildActionExecuter.java:29)
        at org.gradle.tooling.internal.provider.StartParamsValidatingActionExecuter.execute(StartParamsValidatingActionExecuter.java:64)
        at org.gradle.tooling.internal.provider.StartParamsValidatingActionExecuter.execute(StartParamsValidatingActionExecuter.java:29)
        at org.gradle.tooling.internal.provider.SessionFailureReportingActionExecuter.execute(SessionFailureReportingActionExecuter.java:59)
        at org.gradle.tooling.internal.provider.SessionFailureReportingActionExecuter.execute(SessionFailureReportingActionExecuter.java:44)
        at org.gradle.tooling.internal.provider.SetupLoggingActionExecuter.execute(SetupLoggingActionExecuter.java:45)
        at org.gradle.tooling.internal.provider.SetupLoggingActionExecuter.execute(SetupLoggingActionExecuter.java:30)
        at org.gradle.launcher.daemon.server.exec.ExecuteBuild.doBuild(ExecuteBuild.java:67)
        at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.WatchForDisconnection.execute(WatchForDisconnection.java:37)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.ResetDeprecationLogger.execute(ResetDeprecationLogger.java:26)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.RequestStopIfSingleUsedDaemon.execute(RequestStopIfSingleUsedDaemon.java:34)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.ForwardClientInput$2.call(ForwardClientInput.java:74)
        at org.gradle.launcher.daemon.server.exec.ForwardClientInput$2.call(ForwardClientInput.java:72)
        at org.gradle.util.Swapper.swap(Swapper.java:38)
        at org.gradle.launcher.daemon.server.exec.ForwardClientInput.execute(ForwardClientInput.java:72)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.LogAndCheckHealth.execute(LogAndCheckHealth.java:55)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.LogToClient.doBuild(LogToClient.java:62)
        at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.EstablishBuildEnvironment.doBuild(EstablishBuildEnvironment.java:82)
        at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
        at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:122)
        at org.gradle.launcher.daemon.server.exec.StartBuildOrRespondWithBusy$1.run(StartBuildOrRespondWithBusy.java:50)
        at org.gradle.launcher.daemon.server.DaemonStateCoordinator$1.run(DaemonStateCoordinator.java:295)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:63)
        at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:46)
        at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:55)
Caused by: org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$ArtifactResolveException: Could not resolve all files for configuration ':dummy'.
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.rethrowFailure(DefaultConfiguration.java:891)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.access$1500(DefaultConfiguration.java:113)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration$ConfigurationFileCollection.getFiles(DefaultConfiguration.java:865)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.getFiles(DefaultConfiguration.java:383)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration_Decorated.getFiles(Unknown Source)
        at org.gradle.api.internal.file.AbstractFileCollection.iterator(AbstractFileCollection.java:68)
        at build_1j5pmp672rzhsf8if3lg2n5kk$_run_closure4$_closure5.doCall(C:\work\gradle-include-build-zip\zip-consuming-project\build.gradle:18)
        at build_1j5pmp672rzhsf8if3lg2n5kk$_run_closure4$_closure5.doCall(C:\work\gradle-include-build-zip\zip-consuming-project\build.gradle)
        at org.gradle.api.internal.file.collections.BuildDependenciesOnlyFileCollectionResolveContext.add(BuildDependenciesOnlyFileCollectionResolveContext.java:70)
        at org.gradle.api.internal.file.collections.BuildDependenciesOnlyFileCollectionResolveContext.add(BuildDependenciesOnlyFileCollectionResolveContext.java:84)
        at org.gradle.api.internal.file.collections.BuildDependenciesOnlyFileCollectionResolveContext.add(BuildDependenciesOnlyFileCollectionResolveContext.java:84)
        at org.gradle.api.internal.file.collections.DefaultConfigurableFileCollection.visitContents(DefaultConfigurableFileCollection.java:91)
        at org.gradle.api.internal.file.CompositeFileCollection.visitDependencies(CompositeFileCollection.java:166)
        at org.gradle.api.internal.file.collections.DefaultConfigurableFileCollection.visitDependencies(DefaultConfigurableFileCollection.java:97)
        at org.gradle.api.internal.file.CompositeFileCollection$1.visitDependencies(CompositeFileCollection.java:116)
        at org.gradle.api.internal.file.CompositeFileTree$FilteredFileTree.visitDependencies(CompositeFileTree.java:122)
        at org.gradle.api.internal.tasks.CachingTaskDependencyResolveContext$TaskGraphImpl.getNodeValues(CachingTaskDependencyResolveContext.java:90)
        at org.gradle.internal.graph.CachingDirectedGraphWalker$GraphWithEmpyEdges.getNodeValues(CachingDirectedGraphWalker.java:202)
        at org.gradle.internal.graph.CachingDirectedGraphWalker.doSearch(CachingDirectedGraphWalker.java:112)
        at org.gradle.internal.graph.CachingDirectedGraphWalker.findValues(CachingDirectedGraphWalker.java:64)
        at org.gradle.api.internal.tasks.CachingTaskDependencyResolveContext.doResolve(CachingTaskDependencyResolveContext.java:77)
        at org.gradle.api.internal.tasks.CachingTaskDependencyResolveContext.resolve(CachingTaskDependencyResolveContext.java:66)
        ... 82 more
Caused by: org.gradle.internal.resolve.ArtifactNotFoundException: Could not find zip-producing-project.zip (project :zip-producing-project).
        at org.gradle.internal.resolve.result.DefaultBuildableArtifactResolveResult.notFound(DefaultBuildableArtifactResolveResult.java:27)
        at org.gradle.api.internal.artifacts.ivyservice.projectmodule.ProjectDependencyResolver.resolveArtifact(ProjectDependencyResolver.java:146)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.ComponentResolversChain$ArtifactResolverChain.resolveArtifact(ComponentResolversChain.java:121)
        at org.gradle.api.internal.artifacts.ivyservice.ivyresolve.ErrorHandlingArtifactResolver.resolveArtifact(ErrorHandlingArtifactResolver.java:46)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.DefaultArtifactSet$LazyArtifactSource.create(DefaultArtifactSet.java:168)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.DefaultArtifactSet$LazyArtifactSource.create(DefaultArtifactSet.java:155)
        at org.gradle.api.internal.artifacts.DefaultResolvedArtifact.getFile(DefaultResolvedArtifact.java:135)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.ArtifactBackedResolvedVariant$DownloadArtifactFile.run(ArtifactBackedResolvedVariant.java:146)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.ArtifactBackedResolvedVariant$SingleArtifactSet.startVisit(ArtifactBackedResolvedVariant.java:105)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.ParallelResolveArtifactSet$VisitingSet$StartVisitAction.execute(ParallelResolveArtifactSet.java:104)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.ParallelResolveArtifactSet$VisitingSet$StartVisitAction.execute(ParallelResolveArtifactSet.java:94)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.executeInParallel(DefaultBuildOperationExecutor.java:152)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.runAll(DefaultBuildOperationExecutor.java:130)
        at org.gradle.api.internal.artifacts.ivyservice.resolveengine.artifact.ParallelResolveArtifactSet$VisitingSet.visit(ParallelResolveArtifactSet.java:60)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration.visitArtifacts(DefaultLenientConfiguration.java:256)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration.access$500(DefaultLenientConfiguration.java:69)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$2.run(DefaultLenientConfiguration.java:231)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:336)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor$RunnableBuildOperationWorker.execute(DefaultBuildOperationExecutor.java:328)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.execute(DefaultBuildOperationExecutor.java:199)
        at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:110)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration.visitArtifactsWithBuildOperation(DefaultLenientConfiguration.java:228)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration.access$200(DefaultLenientConfiguration.java:69)
        at org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$1.visitArtifacts(DefaultLenientConfiguration.java:133)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration$ConfigurationFileCollection.getFiles(DefaultConfiguration.java:862)
        ... 101 more


* Get more help at https://help.gradle.org

BUILD FAILED in 1s
```
