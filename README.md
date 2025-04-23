# Terraform Azure Network Module

This Terraform module deploys Azure Virtual Networks (VNets) and Subnets based on a specification defined in `network_spec.tf`. The module supports deploying multiple networks dynamically using iterators and loops, following a naming convention for resources.

## Resources Deployed
- **Resource Group**:
  - One per VNet, named as `<vnet-name>-rg` (e.g., `vnet-prod-eastus-rg`).
  - Location is derived from the VNet’s `location` in the spec.
- **Virtual Network (VNet)**:
  - One per entry in `network_spec`, named as specified in the spec (e.g., `vnet-prod-eastus`).
  - Address space and location are taken from the spec.
- **Subnets**:
  - Multiple subnets per VNet, named as `<vnet-name>-<name_suffix>` (e.g., `vnet-prod-eastus-frontend`).
  - Address prefixes are specified in the spec.

## Project Summary
- **Goal**: Create a reusable Terraform parent module to deploy Azure networks with VNets and subnets.
- **Key Features**:
  - Uses a local block in `network_spec.tf` to define network configurations.
  - Supports deploying multiple VNets and subnets using `for_each` loops.
  - Derives resource names dynamically (e.g., resource groups as `<vnet-name>-rg`, subnets as `<vnet-name>-<name_suffix>`).
  - Keeps the spec concise by deriving values like resource group names and subnet names.
- **Files**:
  - `network_spec.tf`: Defines the network specification using a `locals` block.
  - `network.tf`: Contains the Terraform code to deploy resources dynamically.
  - `README.md`: This documentation.

## Usage
1. Define your networks in `network_spec.tf` by modifying the `network_spec` local block.
2. Log in to Azure CLI:
