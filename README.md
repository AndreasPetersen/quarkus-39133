Reproducer for https://github.com/quarkusio/quarkus/issues/39133

## Prerequisite
- A non `mavenCetral` and `gradlePluginCentral` to get Maven packages and Gradle plugins from, e.g. using an internal Artifactory
- An HTTP-proxy to configure in `gradle.properties`

## Steps to Reproduce

1. Run `quarkus update` or `./gradlew quarkusUpdate`
2. Observe that Quarkus fails to update:

```
quarkus update

> Task :quarkusUpdate
quarkusUpdate is experimental, its options and output might change in future versions
Detected project Java version: 21
Detected project Java version: 21
Instructions to update this project from '3.7.4' to '3.8.1':
Recommended Quarkus platform BOM updates:
Update: io.quarkus.platform:quarkus-bom:pom:3.7.4 -> 3.8.1

Extensions from io.quarkus.platform:quarkus-bom:

Resolved io.quarkus:quarkus-updates-recipes:1.0.14 with 1 recipe(s) to update from 3.7.4 to 3.8.1 (initially made for OpenRewrite GRADLE plugin version: 6.7.0)
OpenRewrite recipe generated: /tmp/quarkus-project-recipe-1562820714991535665.yaml



 ------------------------------------------------------------------------
Executing:
/mnt/c/repos/code-with-quarkus/gradlew --console plain --stacktrace --init-script /tmp/openrewrite-init15807579280758196870gradle rewriteRun

Starting a Gradle Daemon, 1 busy and 1 incompatible and 1 stopped Daemons could not be reused, use --status for details
> Task :processResources UP-TO-DATE
> Task :quarkusGenerateCode
> Task :quarkusGenerateCodeDev
> Task :compileJava UP-TO-DATE
> Task :classes UP-TO-DATE
> Task :compileQuarkusTestGeneratedSourcesJava NO-SOURCE
> Task :quarkusGenerateCodeTests
> Task :compileTestJava UP-TO-DATE
> Task :processTestResources NO-SOURCE
> Task :testClasses UP-TO-DATE
> Task :compileIntegrationTestJava NO-SOURCE
> Task :processIntegrationTestResources NO-SOURCE
> Task :integrationTestClasses UP-TO-DATE
> Task :compileNativeTestJava
> Task :compileQuarkusGeneratedSourcesJava NO-SOURCE
> Task :rewriteResolveDependencies FAILED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 9.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

For more on this, please refer to https://docs.gradle.org/8.5/userguide/command_line_interface.html#sec:command_line_warnings in the Gradle documentation.
8 actionable tasks: 5 executed, 3 up-to-date

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':rewriteResolveDependencies'.
> Could not resolve all files for configuration ':detachedConfiguration14'.
   > Could not find junit:junit:.
     Required by:
         project : > org.openrewrite:rewrite-java:8.14.0 > io.github.fastfilter:fastfilter:1.0.2

* Try:
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
> Get more help at https://help.gradle.org.

* Exception is:
org.gradle.api.tasks.TaskExecutionException: Execution failed for task ':rewriteResolveDependencies'.
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.lambda$executeIfValid$1(ExecuteActionsTaskExecuter.java:148)
        at org.gradle.internal.Try$Failure.ifSuccessfulOrElse(Try.java:282)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:146)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:134)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:74)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:42)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:331)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:318)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.lambda$execute$0(DefaultTaskExecutionGraph.java:314)
        at org.gradle.internal.operations.CurrentBuildOperationRef.with(CurrentBuildOperationRef.java:80)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:314)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:303)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:463)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:380)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.AbstractManagedExecutor$1.run(AbstractManagedExecutor.java:47)
Caused by: org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$ArtifactResolveException: Could not resolve all files for configuration ':detachedConfiguration14'.
        at org.gradle.api.internal.artifacts.ResolveExceptionContextualizer.mapFailure(ResolveExceptionContextualizer.java:81)
        at org.gradle.api.internal.artifacts.ResolveExceptionContextualizer.mapFailures(ResolveExceptionContextualizer.java:60)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration$DefaultResolutionHost.mapFailure(DefaultConfiguration.java:2310)
        at org.gradle.api.internal.artifacts.configurations.ResolutionHost.rethrowFailure(ResolutionHost.java:30)
        at org.gradle.api.internal.artifacts.configurations.ResolutionBackedFileCollection.maybeThrowResolutionFailures(ResolutionBackedFileCollection.java:84)
        at org.gradle.api.internal.artifacts.configurations.ResolutionBackedFileCollection.visitContents(ResolutionBackedFileCollection.java:74)
        at org.gradle.api.internal.file.AbstractFileCollection.visitStructure(AbstractFileCollection.java:359)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.visitContents(DefaultConfiguration.java:557)
        at org.gradle.api.internal.file.AbstractFileCollection.getFiles(AbstractFileCollection.java:123)
        at org.gradle.api.internal.artifacts.configurations.DefaultUnlockedConfiguration_Decorated.getFiles(Unknown Source)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.resolve(DefaultConfiguration.java:547)
        at org.openrewrite.gradle.ResolveRewriteDependenciesTask.getResolvedDependencies(ResolveRewriteDependenciesTask.java:111)
        at org.openrewrite.gradle.ResolveRewriteDependenciesTask_Decorated.getResolvedDependencies(Unknown Source)
        at org.openrewrite.gradle.ResolveRewriteDependenciesTask.run(ResolveRewriteDependenciesTask.java:118)
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
        at org.gradle.internal.reflect.JavaMethod.invoke(JavaMethod.java:125)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.doExecute(StandardTaskAction.java:58)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.execute(StandardTaskAction.java:51)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.execute(StandardTaskAction.java:29)
        at org.gradle.api.internal.tasks.execution.TaskExecution$3.run(TaskExecution.java:248)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:29)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:26)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.run(DefaultBuildOperationRunner.java:47)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:68)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeAction(TaskExecution.java:233)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeActions(TaskExecution.java:216)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeWithPreviousOutputFiles(TaskExecution.java:199)
        at org.gradle.api.internal.tasks.execution.TaskExecution.execute(TaskExecution.java:166)
        at org.gradle.internal.execution.steps.ExecuteStep.executeInternal(ExecuteStep.java:105)
        at org.gradle.internal.execution.steps.ExecuteStep.access$000(ExecuteStep.java:44)
        at org.gradle.internal.execution.steps.ExecuteStep$1.call(ExecuteStep.java:59)
        at org.gradle.internal.execution.steps.ExecuteStep$1.call(ExecuteStep.java:56)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.internal.execution.steps.ExecuteStep.execute(ExecuteStep.java:56)
        at org.gradle.internal.execution.steps.ExecuteStep.execute(ExecuteStep.java:44)
        at org.gradle.internal.execution.steps.RemovePreviousOutputsStep.execute(RemovePreviousOutputsStep.java:67)
        at org.gradle.internal.execution.steps.RemovePreviousOutputsStep.execute(RemovePreviousOutputsStep.java:37)
        at org.gradle.internal.execution.steps.CancelExecutionStep.execute(CancelExecutionStep.java:41)
        at org.gradle.internal.execution.steps.TimeoutStep.executeWithoutTimeout(TimeoutStep.java:74)
        at org.gradle.internal.execution.steps.TimeoutStep.execute(TimeoutStep.java:55)
        at org.gradle.internal.execution.steps.CreateOutputsStep.execute(CreateOutputsStep.java:50)
        at org.gradle.internal.execution.steps.CreateOutputsStep.execute(CreateOutputsStep.java:28)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.executeDelegateBroadcastingChanges(CaptureStateAfterExecutionStep.java:100)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.execute(CaptureStateAfterExecutionStep.java:72)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.execute(CaptureStateAfterExecutionStep.java:50)
        at org.gradle.internal.execution.steps.ResolveInputChangesStep.execute(ResolveInputChangesStep.java:40)
        at org.gradle.internal.execution.steps.ResolveInputChangesStep.execute(ResolveInputChangesStep.java:29)
        at org.gradle.internal.execution.steps.BuildCacheStep.executeWithoutCache(BuildCacheStep.java:179)
        at org.gradle.internal.execution.steps.BuildCacheStep.lambda$execute$1(BuildCacheStep.java:70)
        at org.gradle.internal.Either$Right.fold(Either.java:175)
        at org.gradle.internal.execution.caching.CachingState.fold(CachingState.java:59)
        at org.gradle.internal.execution.steps.BuildCacheStep.execute(BuildCacheStep.java:68)
        at org.gradle.internal.execution.steps.BuildCacheStep.execute(BuildCacheStep.java:46)
        at org.gradle.internal.execution.steps.StoreExecutionStateStep.execute(StoreExecutionStateStep.java:36)
        at org.gradle.internal.execution.steps.StoreExecutionStateStep.execute(StoreExecutionStateStep.java:25)
        at org.gradle.internal.execution.steps.RecordOutputsStep.execute(RecordOutputsStep.java:36)
        at org.gradle.internal.execution.steps.RecordOutputsStep.execute(RecordOutputsStep.java:22)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.executeBecause(SkipUpToDateStep.java:91)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.lambda$execute$2(SkipUpToDateStep.java:55)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.execute(SkipUpToDateStep.java:55)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.execute(SkipUpToDateStep.java:37)
        at org.gradle.internal.execution.steps.ResolveChangesStep.execute(ResolveChangesStep.java:65)
        at org.gradle.internal.execution.steps.ResolveChangesStep.execute(ResolveChangesStep.java:36)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsFinishedStep.execute(MarkSnapshottingInputsFinishedStep.java:37)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsFinishedStep.execute(MarkSnapshottingInputsFinishedStep.java:27)
        at org.gradle.internal.execution.steps.ResolveCachingStateStep.execute(ResolveCachingStateStep.java:76)
        at org.gradle.internal.execution.steps.ResolveCachingStateStep.execute(ResolveCachingStateStep.java:37)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:108)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:55)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:71)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:45)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.executeWithNonEmptySources(SkipEmptyWorkStep.java:177)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:81)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:53)
        at org.gradle.internal.execution.steps.RemoveUntrackedExecutionStateStep.execute(RemoveUntrackedExecutionStateStep.java:32)
        at org.gradle.internal.execution.steps.RemoveUntrackedExecutionStateStep.execute(RemoveUntrackedExecutionStateStep.java:21)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsStartedStep.execute(MarkSnapshottingInputsStartedStep.java:38)
        at org.gradle.internal.execution.steps.LoadPreviousExecutionStateStep.execute(LoadPreviousExecutionStateStep.java:36)
        at org.gradle.internal.execution.steps.LoadPreviousExecutionStateStep.execute(LoadPreviousExecutionStateStep.java:23)
        at org.gradle.internal.execution.steps.CleanupStaleOutputsStep.execute(CleanupStaleOutputsStep.java:75)
        at org.gradle.internal.execution.steps.CleanupStaleOutputsStep.execute(CleanupStaleOutputsStep.java:41)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.lambda$execute$2(ExecuteWorkBuildOperationFiringStep.java:66)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.execute(ExecuteWorkBuildOperationFiringStep.java:66)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.execute(ExecuteWorkBuildOperationFiringStep.java:38)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.lambda$execute$0(AssignWorkspaceStep.java:32)
        at org.gradle.api.internal.tasks.execution.TaskExecution$4.withWorkspace(TaskExecution.java:293)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:30)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:21)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:37)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:27)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:47)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:34)
        at org.gradle.internal.execution.impl.DefaultExecutionEngine$1.execute(DefaultExecutionEngine.java:64)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:145)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:134)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:74)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:42)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:331)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:318)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.lambda$execute$0(DefaultTaskExecutionGraph.java:314)
        at org.gradle.internal.operations.CurrentBuildOperationRef.with(CurrentBuildOperationRef.java:80)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:314)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:303)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:463)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:380)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.AbstractManagedExecutor$1.run(AbstractManagedExecutor.java:47)
Caused by: org.gradle.internal.resolve.ModuleVersionNotFoundException: Could not find junit:junit:.
Required by:
    project : > org.openrewrite:rewrite-java:8.14.0 > io.github.fastfilter:fastfilter:1.0.2


BUILD FAILED in 22s




> Task :quarkusUpdate FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':quarkusUpdate'.
> Failed to apply recommended updates

* Try:
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
> Get more help at https://help.gradle.org.

* Exception is:
org.gradle.api.tasks.TaskExecutionException: Execution failed for task ':quarkusUpdate'.
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.lambda$executeIfValid$1(ExecuteActionsTaskExecuter.java:148)
        at org.gradle.internal.Try$Failure.ifSuccessfulOrElse(Try.java:282)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:146)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:134)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:74)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:42)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:331)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:318)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.lambda$execute$0(DefaultTaskExecutionGraph.java:314)
        at org.gradle.internal.operations.CurrentBuildOperationRef.with(CurrentBuildOperationRef.java:80)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:314)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:303)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:463)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:380)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.AbstractManagedExecutor$1.run(AbstractManagedExecutor.java:47)
Caused by: org.gradle.api.GradleException: Failed to apply recommended updates
        at io.quarkus.gradle.tasks.QuarkusUpdate.logUpdates(QuarkusUpdate.java:157)
        at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
        at org.gradle.internal.reflect.JavaMethod.invoke(JavaMethod.java:125)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.doExecute(StandardTaskAction.java:58)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.execute(StandardTaskAction.java:51)
        at org.gradle.api.internal.project.taskfactory.StandardTaskAction.execute(StandardTaskAction.java:29)
        at org.gradle.api.internal.tasks.execution.TaskExecution$3.run(TaskExecution.java:248)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:29)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:26)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.run(DefaultBuildOperationRunner.java:47)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:68)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeAction(TaskExecution.java:233)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeActions(TaskExecution.java:216)
        at org.gradle.api.internal.tasks.execution.TaskExecution.executeWithPreviousOutputFiles(TaskExecution.java:199)
        at org.gradle.api.internal.tasks.execution.TaskExecution.execute(TaskExecution.java:166)
        at org.gradle.internal.execution.steps.ExecuteStep.executeInternal(ExecuteStep.java:105)
        at org.gradle.internal.execution.steps.ExecuteStep.access$000(ExecuteStep.java:44)
        at org.gradle.internal.execution.steps.ExecuteStep$1.call(ExecuteStep.java:59)
        at org.gradle.internal.execution.steps.ExecuteStep$1.call(ExecuteStep.java:56)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.internal.execution.steps.ExecuteStep.execute(ExecuteStep.java:56)
        at org.gradle.internal.execution.steps.ExecuteStep.execute(ExecuteStep.java:44)
        at org.gradle.internal.execution.steps.RemovePreviousOutputsStep.execute(RemovePreviousOutputsStep.java:67)
        at org.gradle.internal.execution.steps.RemovePreviousOutputsStep.execute(RemovePreviousOutputsStep.java:37)
        at org.gradle.internal.execution.steps.CancelExecutionStep.execute(CancelExecutionStep.java:41)
        at org.gradle.internal.execution.steps.TimeoutStep.executeWithoutTimeout(TimeoutStep.java:74)
        at org.gradle.internal.execution.steps.TimeoutStep.execute(TimeoutStep.java:55)
        at org.gradle.internal.execution.steps.CreateOutputsStep.execute(CreateOutputsStep.java:50)
        at org.gradle.internal.execution.steps.CreateOutputsStep.execute(CreateOutputsStep.java:28)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.executeDelegateBroadcastingChanges(CaptureStateAfterExecutionStep.java:100)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.execute(CaptureStateAfterExecutionStep.java:72)
        at org.gradle.internal.execution.steps.CaptureStateAfterExecutionStep.execute(CaptureStateAfterExecutionStep.java:50)
        at org.gradle.internal.execution.steps.ResolveInputChangesStep.execute(ResolveInputChangesStep.java:40)
        at org.gradle.internal.execution.steps.ResolveInputChangesStep.execute(ResolveInputChangesStep.java:29)
        at org.gradle.internal.execution.steps.BuildCacheStep.executeWithoutCache(BuildCacheStep.java:179)
        at org.gradle.internal.execution.steps.BuildCacheStep.lambda$execute$1(BuildCacheStep.java:70)
        at org.gradle.internal.Either$Right.fold(Either.java:175)
        at org.gradle.internal.execution.caching.CachingState.fold(CachingState.java:59)
        at org.gradle.internal.execution.steps.BuildCacheStep.execute(BuildCacheStep.java:68)
        at org.gradle.internal.execution.steps.BuildCacheStep.execute(BuildCacheStep.java:46)
        at org.gradle.internal.execution.steps.StoreExecutionStateStep.execute(StoreExecutionStateStep.java:36)
        at org.gradle.internal.execution.steps.StoreExecutionStateStep.execute(StoreExecutionStateStep.java:25)
        at org.gradle.internal.execution.steps.RecordOutputsStep.execute(RecordOutputsStep.java:36)
        at org.gradle.internal.execution.steps.RecordOutputsStep.execute(RecordOutputsStep.java:22)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.executeBecause(SkipUpToDateStep.java:91)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.lambda$execute$2(SkipUpToDateStep.java:55)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.execute(SkipUpToDateStep.java:55)
        at org.gradle.internal.execution.steps.SkipUpToDateStep.execute(SkipUpToDateStep.java:37)
        at org.gradle.internal.execution.steps.ResolveChangesStep.execute(ResolveChangesStep.java:65)
        at org.gradle.internal.execution.steps.ResolveChangesStep.execute(ResolveChangesStep.java:36)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsFinishedStep.execute(MarkSnapshottingInputsFinishedStep.java:37)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsFinishedStep.execute(MarkSnapshottingInputsFinishedStep.java:27)
        at org.gradle.internal.execution.steps.ResolveCachingStateStep.execute(ResolveCachingStateStep.java:76)
        at org.gradle.internal.execution.steps.ResolveCachingStateStep.execute(ResolveCachingStateStep.java:37)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:108)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:55)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:71)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:45)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.executeWithNonEmptySources(SkipEmptyWorkStep.java:177)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:81)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:53)
        at org.gradle.internal.execution.steps.RemoveUntrackedExecutionStateStep.execute(RemoveUntrackedExecutionStateStep.java:32)
        at org.gradle.internal.execution.steps.RemoveUntrackedExecutionStateStep.execute(RemoveUntrackedExecutionStateStep.java:21)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsStartedStep.execute(MarkSnapshottingInputsStartedStep.java:38)
        at org.gradle.internal.execution.steps.LoadPreviousExecutionStateStep.execute(LoadPreviousExecutionStateStep.java:36)
        at org.gradle.internal.execution.steps.LoadPreviousExecutionStateStep.execute(LoadPreviousExecutionStateStep.java:23)
        at org.gradle.internal.execution.steps.CleanupStaleOutputsStep.execute(CleanupStaleOutputsStep.java:75)
        at org.gradle.internal.execution.steps.CleanupStaleOutputsStep.execute(CleanupStaleOutputsStep.java:41)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.lambda$execute$2(ExecuteWorkBuildOperationFiringStep.java:66)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.execute(ExecuteWorkBuildOperationFiringStep.java:66)
        at org.gradle.internal.execution.steps.ExecuteWorkBuildOperationFiringStep.execute(ExecuteWorkBuildOperationFiringStep.java:38)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.lambda$execute$0(AssignWorkspaceStep.java:32)
        at org.gradle.api.internal.tasks.execution.TaskExecution$4.withWorkspace(TaskExecution.java:293)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:30)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:21)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:37)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:27)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:47)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:34)
        at org.gradle.internal.execution.impl.DefaultExecutionEngine$1.execute(DefaultExecutionEngine.java:64)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:145)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:134)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:74)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:204)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:199)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:66)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$2.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:157)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:59)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:53)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:73)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:42)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:331)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:318)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.lambda$execute$0(DefaultTaskExecutionGraph.java:314)
        at org.gradle.internal.operations.CurrentBuildOperationRef.with(CurrentBuildOperationRef.java:80)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:314)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:303)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:463)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:380)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.AbstractManagedExecutor$1.run(AbstractManagedExecutor.java:47)
Caused by: io.quarkus.devtools.project.update.rewrite.QuarkusUpdateExitErrorException: The command to update the project exited with an error, see the execution logs above for more details
        at io.quarkus.devtools.project.update.rewrite.QuarkusUpdateCommand.executeCommand(QuarkusUpdateCommand.java:223)
        at io.quarkus.devtools.project.update.rewrite.QuarkusUpdateCommand.runGradleUpdate(QuarkusUpdateCommand.java:95)
        at io.quarkus.devtools.project.update.rewrite.QuarkusUpdateCommand.handle(QuarkusUpdateCommand.java:54)
        at io.quarkus.devtools.commands.handlers.UpdateProjectCommandHandler.execute(UpdateProjectCommandHandler.java:123)
        at io.quarkus.devtools.commands.UpdateProject.execute(UpdateProject.java:83)
        at io.quarkus.gradle.tasks.QuarkusUpdate.logUpdates(QuarkusUpdate.java:155)
        ... 120 more


BUILD FAILED in 27s
1 actionable task: 1 executed
```
