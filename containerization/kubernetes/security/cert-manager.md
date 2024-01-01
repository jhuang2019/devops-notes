# Cert-manager

## What is cert-manager
* Cert-manager is a powerful and extensible X.509 certificate controller for Kubernetes and OpenShift workloads. 
* It will obtain certificates from a variety of Issuers, including  public issuers and private issuers, and ensure the certificates are valid and up-to-date.
* It also renews certificates at a configured time before expiry.
* X.509 is a standard format for public key certificates. 

## Installation
1. How to install cert-manager

There are various ways you can install cert-manager. 
* Default static install for kubernetes
```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/xxxxxx
```
* Helm for kubernets
    * Installing with Helm
        * Add the Helm repository
        * Update your local Helm chart repository cache
        * Install `CustomResourceDefinitions` (CRDs)
            * Option 1: intalling CRDs with `kubectl`
            * Option 2: installing CRDs as part of the Helm release
        * Install cert-manager
    * Installing cert-manager as subchart (use this option in the project)
* OperatorHub for OpenShift

2. CRD considerations
* kubectl installation
* helm installation
* installation advice
    * For Safety, install CRDs outside of Helm, e.g. `kubectl` installation (use this option in the project)
    * For Ease of use, install CRDs with `helm` installation.

3. How to upgrade cert-manager
* Upgrading with Helm
* Upgrading using static manifests
```
kubectl apply -f xxxxxxx
```

## Issuer configuration
* The first thing you'll need to configure after you've installed cert-manager is an `Issuer` or a `ClusterIssuer`.
* cert-manager comes with a number of built-in certificate issuers which are denoted by being in the `cert-manager.io` group. 
* One of the popular issuers is adcs-issuer, i.e. Microsoft Active Directory Certificate Service.

## Requesting certificates
Once an Issuer has been configured, you're ready to issue your certificate.


## Distributing trust
## Defining policies
## References
* https://cert-manager.io/docs/
