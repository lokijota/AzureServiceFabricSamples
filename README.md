# AzureServiceFabricSamples
My tests and samples with Azure Service Fabric, Preview version 1.4.87.

My goal is mainly to explore the Actor programming model, with IoT scenarios or with what traditionally would be stateless services.

Starting with base samples from Microsoft: (https://azure.microsoft.com/en-us/documentation/articles/service-fabric-create-your-first-application-in-visual-studio/)

## Microsoft Samples Setup Problems

I had several problems running the simplest of samples, the Stateful Service one linked above. Solutions as follows.

1) VS2015 has to be run as an admin;

2) when starting Debug (F5) of the project for the first time, I was getting  errors setting up the cluster. A Microsoft forum post (https://social.msdn.microsoft.com/Forums/expression/en-US/a74bf0f7-3106-4b48-b48f-4ea250a24964/cluster-setup-errors-connectservicefabriccluster-a-communication-error-caused-the-operation-to?forum=AzureServiceFabric) suggested this which solved this issue:

run *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\CleanCluster.ps1*

run *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1*

3) The troubleshooting guide (https://github.com/Azure/azure-content/blob/master/articles/service-fabric/service-fabric-diagnostics-troubleshoot-common-scenarios.md) didn't help.

4) After this I starting having an error also described in the comments of another tutorial (https://azure.microsoft.com/en-us/documentation/articles/service-fabric-reliable-services-quick-start/) , but where no fix is proposed:

fabric:/MyApplication/MyStatefulService is not ready, 1 partitions remaining.

fabric:/MyApplication/MyStatefulService is not ready, 1 partitions remaining.

Checking the event viewer, I found a FileNotFoundException, and further down, a message saying that there was not enough free space on disk. I had 2Gb free, but turns out Service Fabric requires 8Gb free to run. This was the problem, and after I free'd space the project ran fine.

5) Finally, after getting the sample running, the Diagnostics window in VS2015 was supposed to show me the applicational log, the result of the calls to ServiceEventSource.Current.ServiceMessage(), but nothing was visible. Turns out I had to add the following as a provider in the diagnostics window: MyCompany-MyApplication-MyStatefulService . I think this was supposed to be added automatically when debugging, but that's not happening.


## Some helpful information (cheat-sheet)

1) To run the commands from here: (https://azure.microsoft.com/en-us/documentation/articles/service-fabric-understand-and-troubleshoot-with-system-health-reports)

you first have to run the followin in the powershell command line:

Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000

2) Keep in mind the following folders:

*C:\Program Files\Microsoft SDKs\Service Fabric\* - where the SDK is installed
*C:\SfDevCluster* - where the local development cluster is installed.
