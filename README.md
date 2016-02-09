# AzureServiceFabricSamples
My tests and samples with Azure Service Fabric, Preview version 1.4.87.

My goal is mainly to explore the Actor programming model, with IoT scenarios or with what traditionally would be stateless services.

Starting with base samples from Microsoft: https://azure.microsoft.com/en-us/documentation/articles/service-fabric-create-your-first-application-in-visual-studio/

Note:

I'm actually having several problems running the simplest of samples.

1) VS2015 has to be run as an admin;
2) when starting DEbug (F5) for the first time, I get errors setting up the cluster. A Microsoft forum post (https://social.msdn.microsoft.com/Forums/expression/en-US/a74bf0f7-3106-4b48-b48f-4ea250a24964/cluster-setup-errors-connectservicefabriccluster-a-communication-error-caused-the-operation-to?forum=AzureServiceFabric) suggested this which solved this issue:

run C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\CleanCluster.ps1
run C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1

3) now I'm having an error that is also described in the comments of another tutorial (https://azure.microsoft.com/en-us/documentation/articles/service-fabric-reliable-services-quick-start/) , but is unfixed:

fabric:/HelloWorldApplication/HelloWorld is not ready, 1 partitions remaining.
fabric:/HelloWorldApplication/HelloWorldStateful is not ready, 1 partitions remaining.
