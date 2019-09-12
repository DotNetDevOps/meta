# meta
DotNetDevOps - Resources for transforming your organization into the new era



# DotNetDevOps Architecture Principles

The following repository contains a compiled set of Achitecture Principles, that teams delivering software might use as guidelines or ruleset for how they design and deliver their solutions.

The focus is mainly around cloud arhitectures and microservices.

Each Principle has its own unique id and resource link, such they can be cherry picked.

## DotNetDevOps Microservices
We try in this document to define a termonology that can be used for talking about your microservice architecture.

### ServiceProvider

A service provider is a set of apis that are deployed together under a namespace (ServiceProvider Id). /Providers/{ServiceProviderId}/ResourceType ect.
A service provider do have versions and each version is hosted seperately and routed based on gateway inspection of api version.