# InstantiateErrorAGP
Sample repository which demonstrates linting issues with AGP >= 7.0.0

# Description
In the following scenario :

- An activity in a module A extends an activity in a module B
- The activity in the module B is an abstract class 
- The activity in the module B extends AppCompatActivity
- Minify is enabled
  
Environment used :
- Java 11
- AGP >= 0
- Gradle 7.0.2
- Android Studio Arctic Fox | 2020.3.1 Patch 4
- Build #AI-203.7717.56.2031.7935034, built on November 21, 2021
- Runtime version: 11.0.10+0-b96-7281165 x86_64
- VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
- macOS 11.5.2
- GC: G1 Young Generation, G1 Old Generation
- Memory: 2048M
- Cores: 8
- Registry: external.system.auto.import.disabled=true
- Non-Bundled Plugins: Dart, org.jetbrains.kotlin, io.flutter, org.intellij.plugins.markdown

The app:lintVitalRelease task will fail, saying that the activity in the module A should extend android.app.Activity.

The issue is not happening with 4.2.0 <= AGP <= 4.2.2 (checkout the git branch 4.2.2 to compare)

# Steps to reproduce
- Clone the repository
- Open a prompt and execute

```bash
./gradlew assembleRelease --stacktrace
```

The build fails and the following error message should be displayed following *app:lintVitalRelease* :

```bash
> Task :app:lintVitalRelease FAILED
/Users/tboutin/AndroidStudioProjects/InstantiateErrorAGP/app/src/main/AndroidManifest.xml:13: Error: MainActivity must extend android.app.Activity [Instantiatable]
            android:name=".MainActivity"
                          ~~~~~~~~~~~~~

   Explanation for issues of type "Instantiatable":
   Activities, services, broadcast receivers etc. registered in the manifest
   file (or for custom views, in a layout file) must be "instantiatable" by
   the system, which means that the class must be public, it must have an
   empty public constructor, and if it's an inner class, it must be a static
   inner class.

1 errors, 0 warnings
Lint found fatal errors while assembling a release target.

To proceed, either fix the issues identified by lint, or modify your build script as follows:
...
android {
    lintOptions {
        checkReleaseBuilds false
        // Or, if you prefer, you can continue to check for errors in release builds,
        // but continue the build even when errors are found:
        abortOnError false
    }
}
...

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:lintVitalRelease'.
> A failure occurred while executing com.android.build.gradle.internal.lint.AndroidLintTask$AndroidLintLauncherWorkAction
   > There was a failure while executing work items
      > A failure occurred while executing com.android.build.gradle.internal.lint.AndroidLintWorkAction
         > Lint found fatal errors while assembling a release target.

* Try:
Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Exception is:
org.gradle.api.tasks.TaskExecutionException: Execution failed for task ':app:lintVitalRelease'.
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.lambda$executeIfValid$1(ExecuteActionsTaskExecuter.java:187)
        at org.gradle.internal.Try$Failure.ifSuccessfulOrElse(Try.java:268)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:185)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:173)
        at org.gradle.api.internal.tasks.execution.CleanupStaleOutputsExecuter.execute(CleanupStaleOutputsExecuter.java:109)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:56)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:74)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:408)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:395)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:388)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:374)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.lambda$run$0(DefaultPlanExecutor.java:127)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:191)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.executeNextNode(DefaultPlanExecutor.java:182)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:124)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:48)
        at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:56)
Caused by: org.gradle.workers.internal.DefaultWorkerExecutor$WorkExecutionException: A failure occurred while executing com.android.build.gradle.internal.lint.AndroidLintTask$AndroidLintLauncherWorkAction
        at org.gradle.workers.internal.DefaultWorkerExecutor.lambda$submitWork$2(DefaultWorkerExecutor.java:208)
        at org.gradle.internal.work.DefaultConditionalExecutionQueue$ExecutionRunner.runExecution(DefaultConditionalExecutionQueue.java:214)
        at org.gradle.internal.work.DefaultConditionalExecutionQueue$ExecutionRunner.runBatch(DefaultConditionalExecutionQueue.java:164)
        at org.gradle.internal.work.DefaultConditionalExecutionQueue$ExecutionRunner.run(DefaultConditionalExecutionQueue.java:131)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:48)
        at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:56)
Caused by: org.gradle.workers.WorkerExecutionException: There was a failure while executing work items
        at org.gradle.workers.internal.DefaultWorkerExecutor.workerExecutionException(DefaultWorkerExecutor.java:270)
        at org.gradle.workers.internal.DefaultWorkerExecutor.await(DefaultWorkerExecutor.java:252)
        at org.gradle.workers.internal.NoIsolationWorkerFactory$1.lambda$execute$0(NoIsolationWorkerFactory.java:72)
        at org.gradle.workers.internal.AbstractWorker$1.call(AbstractWorker.java:44)
        at org.gradle.workers.internal.AbstractWorker$1.call(AbstractWorker.java:41)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.workers.internal.AbstractWorker.executeWrappedInBuildOperation(AbstractWorker.java:41)
        at org.gradle.workers.internal.NoIsolationWorkerFactory$1.execute(NoIsolationWorkerFactory.java:59)
        at org.gradle.workers.internal.DefaultWorkerExecutor.lambda$submitWork$2(DefaultWorkerExecutor.java:206)
        ... 6 more
Caused by: org.gradle.workers.internal.DefaultWorkerExecutor$WorkExecutionException: A failure occurred while executing com.android.build.gradle.internal.lint.AndroidLintWorkAction
        at org.gradle.workers.internal.DefaultWorkerExecutor$WorkItemExecution.waitForCompletion(DefaultWorkerExecutor.java:342)
        at org.gradle.internal.work.DefaultAsyncWorkTracker.waitForItemsAndGatherFailures(DefaultAsyncWorkTracker.java:142)
        at org.gradle.internal.work.DefaultAsyncWorkTracker.waitForItemsAndGatherFailures(DefaultAsyncWorkTracker.java:90)
        at org.gradle.internal.work.DefaultAsyncWorkTracker.waitForAll(DefaultAsyncWorkTracker.java:80)
        at org.gradle.internal.work.DefaultAsyncWorkTracker.waitForCompletion(DefaultAsyncWorkTracker.java:68)
        at org.gradle.workers.internal.DefaultWorkerExecutor.await(DefaultWorkerExecutor.java:250)
        ... 22 more
Caused by: java.lang.RuntimeException: Lint found fatal errors while assembling a release target.
        at com.android.build.gradle.internal.lint.AndroidLintWorkAction.execute(AndroidLintWorkAction.kt:107)
        at org.gradle.workers.internal.DefaultWorkerServer.execute(DefaultWorkerServer.java:63)
        at org.gradle.workers.internal.NoIsolationWorkerFactory$1$1.create(NoIsolationWorkerFactory.java:66)
        at org.gradle.workers.internal.NoIsolationWorkerFactory$1$1.create(NoIsolationWorkerFactory.java:62)
        at org.gradle.internal.classloader.ClassLoaderUtils.executeInClassloader(ClassLoaderUtils.java:97)
        at org.gradle.workers.internal.NoIsolationWorkerFactory$1.lambda$execute$0(NoIsolationWorkerFactory.java:62)
        ... 21 more


* Get more help at https://help.gradle.org

Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/7.0.2/userguide/command_line_interface.html#sec:command_line_warnings

BUILD FAILED in 8s
```