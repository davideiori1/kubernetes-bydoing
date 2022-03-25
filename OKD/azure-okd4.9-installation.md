# INSTALL OKD4.9 ON AZURE

Following guide is based on the official [installation procedure](https://docs.okd.io/4.9/installing/installing_azure/preparing-to-install-on-azure.html).

## PREREQUISITE
- read the [core concept](./core-concepts.md) guide
- **An Azure account**: It is possible to create an azure account for **free** with a budget of 200$. Keep in mind that a Azure has by default set some [limits](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits) mostly to prevent unexpteced costs from happening. Those limits, or quotas, can be adjusted **BUT** Free Trial subscriptions aren't eligible for limit or quota increases and that could force us to upgrade to a Pay-As-You-Go subscription. __This is not what I did and rest of the guide will show you how to install a OKD cluster within limits and using a free trial subscription__.
- Keeping in mind what told before, our next challenge is the choice of the installation type. Like said in the [core concept](./core-concepts.md), we will go for the **IPI** method of installation, the one suggested by Red Hat itself, but there are different types of istallation which are possible to execute on Azure:

| Choice | Type | Note  |
|--------|------|-------|
|[ ] |[Default](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-default.html#installing-azure-default)  | This is the quickets way to get a OKD cluster on Azure **BUT** you won't have the possibility to customize you install-config file and that will lead to a cluster that will exceed the Azure limits which are not adjustable if you are using a Free-trial subscription. IPI will fail.|
|[X] |[Custom](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-customizations.html#installing-azure-customizations)  | We need to use a custom install-config in order to create a light-weight cluster in order not to adjust the limits/quotas |
|[ ] |[Network customization](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-network-customizations.html#installing-azure-network-customizations) | This is out-of-scope this exercise|
|[ ] |[Private Cluster](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-private.html#installing-azure-private)| This exercise will deploy a public cluster as it is intended for learning purpose and won't be used for storing sensitive data or running special workloads, so no need to create a private cluster|
|[X] |[Existing VNET](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-vnet.html#installing-azure-vnet)| We go for this option just for the sake of customizing a bit more our installer|

### AZURE ACCOUNT CONFIGURATION
After having chosen the type of installation, we need to [configure our Azure account](https://docs.okd.io/4.9/installing/installing_azure/installing-azure-account.html#installing-azure-account). You do not need to follow the linked guide, just keep reading as I will walk you through the task you need to perform for our specific type of installation.

#### CONFIGURING A PUBLIC DNS ZONE IN AZURE
Our cluster will be publicy available over the Internet, therefore to install OKD, the Microsoft Azure account you use must have a dedicated public hosted DNS zone in your account. This zone must be authoritative for the domain. This service provides cluster DNS resolution and name lookup for external connections to the cluster.
- We need to have a public domain. If you do not have one, you can purchase a domain for **free** at [register.it](https://www.register.it/)
- Now that you have a DNS domain, in my case `learningk8s.me`, you can use Azure DNS to host it and manage your DNS records (following steps are taken from this [tutorial](https://docs.microsoft.com/en-us/azure/dns/dns-delegate-domain-azure-dns):
  - Create your parent DNS zone: 
-If you are using an existing domain,  and registrar, migrate its DNS to Azure. See Migrate an active DNS name to Azure App Service in the Azure documentation.

-Configure DNS for your domain. Follow the steps in the Tutorial: Host your domain in Azure DNS in the Azure documentation to create a public hosted zone for your domain or subdomain, extract the new authoritative name servers, and update the registrar records for the name servers that your domain uses.
Use an appropriate root domain, such as openshiftcorp.com, or subdomain, such as clusters.openshiftcorp.com.

-If you use a subdomain, follow your company’s procedures to add its delegation records to the parent domain.



https://docs.okd.io/4.9/installing/installing_azure/installing-azure-customizations.html
