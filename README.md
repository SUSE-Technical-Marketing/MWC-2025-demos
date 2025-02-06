# SUSE Edge for Telco: Scalable Cluster Lifecycle Management Demo

This demo showcases SUSE Edge for Telco's powerful cluster lifecycle management capabilities. We'll walk through deploying and managing Kubernetes clusters across multiple regions and availability zones, leveraging Cluster API (CAPI), Metal3 for bare metal provisioning, and the Rancher Turtles addon.  We'll also demonstrate the seamless integration of Fleet and GitOps to implement a complete management-as-code workflow.

[![Demo MWC 2025](/resources/images/Demo-MWC2025.png "Lab structure and components")](/resources/images/Demo-MWC2025.png)  *(Click image to enlarge)*

## Demo Overview

This demo focuses on two key regions:

* **EMEA-SPA Region:** This region comprises two availability zones (AZs). Each AZ will deploy clusters using distinct Cluster Classes.  We'll demonstrate how to upgrade all clusters within an AZ by modifying the Cluster Class and associated manifests, showcasing the power of declarative management.

* **EMEA-GER Region:**  This region simulates a large-scale bare metal deployment (200 servers) using emulated clusters managed by Fleet.  This highlights SUSE Edge for Telco's ability to handle massive cluster deployments.

## Workflow

While the management cluster deployment is outside the scope of this demo, it worth noting that was deployed as an appliance including SL Micro, RKE 2, Rancher, Turtles (CAPI), Metal3, SUSE Storage (Longhorn), and SUSE Security (NeuVector) using an Edge Image Builder-created ISO.

In this demo we will run the following key steps:

1. **CAPI UI Extension Installation:**  We'll begin by installing the CAPI UI extension for simplified cluster management.

2. **Cluster Management Overview:**  We'll explore the cluster management interface, showcasing deployed clusters, Bare Metal Host (BMH) objects, and other relevant components.

3. **Git Repository Overview:**  We'll review the Git repository structure, branches, and components used for deployment, emphasizing the management-as-code approach.

4. **EMEA-GER Region Deployment (Fleet):** We'll deploy 200 emulated clusters in the EMEA-GER region using Fleet, demonstrating large-scale deployment capabilities.

5. **EMEA-GER Region Deployment Monitoring:** We'll monitor the deployment progress of the 200 emulated servers.

6. **Benefits of using clusterClass:** We'll discuss the advantages of using Cluster Class manifests over standard manifests for simplified and consistent deployments.

7. **EMEA-SPA Region Deployment (CAPI & GitOps):**
    * We'll create two distinct Cluster Classes for the two AZs in the EMEA-SPA region.
    * The manifests for these clusters will reside in the `emea-spa` branch of the demo repository. We will use diferent labels for the different cluster instances depending on the AZ they're located, these labels will be used by Fleet to know what to deploy and where.
    * Initially, the branch will be empty. In the first commit we will send the BMH manifests, Fleet will deploy them to the management cluster triggering the process. Metal3 will invoque the Ironic Python Agent (IPA) that will connect to the BMCs in order to inspect the hardware and determine the availability.
    * In a second commit we will push the manifests for instantiating the clusterClasses. Fleet will detect the changes, triggering CAPI to initiate the deployment process, installing the SL Micro and Kubernetes demonstrating GitOps in action.

8. **Day Two Operations:**
    * **Part 1: Application Upgrade:** We'll upgrade an application within AZ1 using the Cluster Class, showcasing streamlined application lifecycle management.
    * **Part 2: Kubernetes Upgrade:** We'll modify manifests for the instances in AZ2 to trigger a Kubernetes upgrade across all clusters within the AZ using CAPI and the management-as-code principles.

## Learn More

For more information about SUSE Edge for Telco, please visit [link to your product page].

## Contributing

[Optional: Add contribution guidelines here if applicable.]