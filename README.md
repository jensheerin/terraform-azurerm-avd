# Microsoft Verified Terraform Module

The Verified Terraform module is a template repository to help developers create their own Terraform Module.

As we've used Microsoft 1ES Runners Pool as our acceptance test runner, **only Microsoft members could use this template for now**.

Enjoy it by following steps:

1. Use [this template](https://github.com/Azure/terraform-verified-module) to create your repository.
2. Read [Onboard 1ES hosted Github Runners Pool through Azure Portal](https://eng.ms/docs/cloud-ai-platform/devdiv/one-engineering-system-1es/1es-docs/1es-github-runners/createpoolportal), install [1ES Resource Management](https://github.com/apps/1es-resource-management) on your repo.
3. Add a Github [Environment](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment) named **acctests** in your repo, setup [**Required Reviewers**](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment#required-reviewers).
4. Update [`acc-test.yaml`](.github/workflows/acc-test.yaml), modify `runs-on: [self-hosted, 1ES.Pool=<YOUR_REPO_NAME>]` with your 1es runners' pool name (basically it's your repo's name).
5. Write Terraform code in a new branch.
6. Run `docker run --rm -v ${pwd}:/src -w /src mcr.microsoft.com/azterraform:latest make pre-commit` to format the code.
7. Run `docker run --rm -v $(pwd):/src -w /src mcr.microsoft.com/azterraform:latest make pr-check` to run the check in local.
8. Create a pull request for the main branch.
    * CI pr-check will be executed automatically.
    * Once pr-check was passed, with manually approval, the e2e test and version upgrade test would be executed.
9. Merge pull request.
10. Enjoy it!

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name                                                                | Version   |
|---------------------------------------------------------------------|-----------|
| <a name="requirement_azuread"></a> [azuread](#requirement\_azuread) | ~> 2.25.0 |

## Providers

| Name                                                          | Version   |
|---------------------------------------------------------------|-----------|
| <a name="provider_azuread"></a> [azuread](#provider\_azuread) | ~> 2.25.0 |
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | n/a       |
| <a name="provider_random"></a> [random](#provider\_random)    | n/a       |

## Modules

No modules.

## Resources

| Name                                                                                                                                                                                                              | Type        |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| [azurerm_monitor_diagnostic_setting.avd-dag1](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting)                                                         | resource    |
| [azurerm_monitor_diagnostic_setting.avd-hp1](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting)                                                          | resource    |
| [azurerm_monitor_diagnostic_setting.avd-wksp1](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting)                                                        | resource    |
| [azurerm_role_assignment.power](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment)                                                                                  | resource    |
| [azurerm_virtual_desktop_application_group.dag](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_application_group)                                                | resource    |
| [azurerm_virtual_desktop_host_pool.hostpool](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_host_pool)                                                           | resource    |
| [azurerm_virtual_desktop_host_pool_registration_info.registrationinfo](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_host_pool_registration_info)               | resource    |
| [azurerm_virtual_desktop_scaling_plan.scplan](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_scaling_plan)                                                       | resource    |
| [azurerm_virtual_desktop_workspace.workspace](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_workspace)                                                          | resource    |
| [azurerm_virtual_desktop_workspace_application_group_association.ws-dag](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_desktop_workspace_application_group_association) | resource    |
| [random_uuid.example](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/uuid)                                                                                                        | resource    |
| [azuread_service_principal.spn](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/service_principal)                                                                             | data source |
| [azurerm_log_analytics_workspace.lawksp](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/log_analytics_workspace)                                                              | data source |
| [azurerm_role_definition.power_role](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/role_definition)                                                                          | data source |

## Inputs

| Name                                                                                                              | Description                                                               | Type           | Default | Required |
|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|----------------|---------|:--------:|
| <a name="input_aad_group_name"></a> [aad\_group\_name](#input\_aad\_group\_name)                                  | Azure Active Directory Group for AVD users                                | `string`       | n/a     |   yes    |
| <a name="input_allow_list_ip"></a> [allow\_list\_ip](#input\_allow\_list\_ip)                                     | List of allowed IP Addresses                                              | `list(string)` | n/a     |   yes    |
| <a name="input_avdLocation"></a> [avdLocation](#input\_avdLocation)                                               | Location of the resource group.                                           | `any`          | n/a     |   yes    |
| <a name="input_avd_users"></a> [avd\_users](#input\_avd\_users)                                                   | AVD users                                                                 | `any`          | n/a     |   yes    |
| <a name="input_avdshared_subscription_id"></a> [avdshared\_subscription\_id](#input\_avdshared\_subscription\_id) | Spoke Subscription id                                                     | `string`       | n/a     |   yes    |
| <a name="input_dag"></a> [dag](#input\_dag)                                                                       | Name of the Azure Virtual Desktop desktop application group               | `string`       | n/a     |   yes    |
| <a name="input_dns_servers"></a> [dns\_servers](#input\_dns\_servers)                                             | Custom DNS configuration                                                  | `list(string)` | n/a     |   yes    |
| <a name="input_domain_name"></a> [domain\_name](#input\_domain\_name)                                             | Name of the domain to join                                                | `string`       | n/a     |   yes    |
| <a name="input_domain_password"></a> [domain\_password](#input\_domain\_password)                                 | Password of the user to authenticate with the domain                      | `string`       | n/a     |   yes    |
| <a name="input_domain_user"></a> [domain\_user](#input\_domain\_user)                                             | Username for domain join (do not include domain name as this is appended) | `string`       | n/a     |   yes    |
| <a name="input_fw_policy"></a> [fw\_policy](#input\_fw\_policy)                                                   | Name of the firewall policy                                               | `string`       | n/a     |   yes    |
| <a name="input_gallery_name"></a> [gallery\_name](#input\_gallery\_name)                                          | Name of the shared image gallery name                                     | `string`       | n/a     |   yes    |
| <a name="input_hostpool"></a> [hostpool](#input\_hostpool)                                                        | Name of the Azure Virtual Desktop host pool                               | `string`       | n/a     |   yes    |
| <a name="input_hub_connectivity_rg"></a> [hub\_connectivity\_rg](#input\_hub\_connectivity\_rg)                   | The resource group for hub connectivity resources                         | `string`       | n/a     |   yes    |
| <a name="input_hub_dns_zone_rg"></a> [hub\_dns\_zone\_rg](#input\_hub\_dns\_zone\_rg)                             | The resource group for the hub DNS zone                                   | `any`          | n/a     |   yes    |
| <a name="input_hub_subscription_id"></a> [hub\_subscription\_id](#input\_hub\_subscription\_id)                   | Hub Subscription id                                                       | `string`       | n/a     |   yes    |
| <a name="input_hub_vnet"></a> [hub\_vnet](#input\_hub\_vnet)                                                      | Name of domain controller vnet                                            | `string`       | n/a     |   yes    |
| <a name="input_identity_rg"></a> [identity\_rg](#input\_identity\_rg)                                             | Name of the Resource group in which to identity resources are deployed    | `string`       | n/a     |   yes    |
| <a name="input_identity_subscription_id"></a> [identity\_subscription\_id](#input\_identity\_subscription\_id)    | identity Subscription id                                                  | `string`       | n/a     |   yes    |
| <a name="input_identity_vnet"></a> [identity\_vnet](#input\_identity\_vnet)                                       | Name of the vnet in which to identity resources are deployed              | `string`       | n/a     |   yes    |
| <a name="input_image_name"></a> [image\_name](#input\_image\_name)                                                | Name of the custome image to use                                          | `string`       | n/a     |   yes    |
| <a name="input_image_rg"></a> [image\_rg](#input\_image\_rg)                                                      | Image Gallery resource group                                              | `string`       | n/a     |   yes    |
| <a name="input_local_admin_username"></a> [local\_admin\_username](#input\_local\_admin\_username)                | local admin username                                                      | `string`       | n/a     |   yes    |
| <a name="input_next_hop_ip"></a> [next\_hop\_ip](#input\_next\_hop\_ip)                                           | Next hop IP address                                                       | `string`       | n/a     |   yes    |
| <a name="input_nsg"></a> [nsg](#input\_nsg)                                                                       | Name of the nsg                                                           | `string`       | n/a     |   yes    |
| <a name="input_ou_path"></a> [ou\_path](#input\_ou\_path)                                                         | Distinguished name of the organizational unit for the session host        | `any`          | n/a     |   yes    |
| <a name="input_pag"></a> [pag](#input\_pag)                                                                       | Name of the Azure Virtual Desktop remote application group                | `string`       | n/a     |   yes    |
| <a name="input_personalpool"></a> [personalpool](#input\_personalpool)                                            | Name of the Azure Virtual Desktop host pool                               | `string`       | n/a     |   yes    |
| <a name="input_pesnet"></a> [pesnet](#input\_pesnet)                                                              | Name of subnet                                                            | `string`       | n/a     |   yes    |
| <a name="input_pesubnet_range"></a> [pesubnet\_range](#input\_pesubnet\_range)                                    | Address range for private endpoints subnet                                | `list(string)` | n/a     |   yes    |
| <a name="input_prefix"></a> [prefix](#input\_prefix)                                                              | Prefix of the name under 5 characters                                     | `string`       | n/a     |   yes    |
| <a name="input_pworkspace"></a> [pworkspace](#input\_pworkspace)                                                  | Name of the Azure Virtual Desktop Personal workspace                      | `string`       | n/a     |   yes    |
| <a name="input_rag"></a> [rag](#input\_rag)                                                                       | Name of the Azure Virtual Desktop remote application group                | `string`       | n/a     |   yes    |
| <a name="input_raghostpool"></a> [raghostpool](#input\_raghostpool)                                               | Name of the Azure Virtual Desktop remote app group                        | `string`       | n/a     |   yes    |
| <a name="input_ragworkspace"></a> [ragworkspace](#input\_ragworkspace)                                            | Name of the Azure Virtual Desktop workspace                               | `string`       | n/a     |   yes    |
| <a name="input_rdsh_count"></a> [rdsh\_count](#input\_rdsh\_count)                                                | Number of AVD machines to deploy                                          | `any`          | n/a     |   yes    |
| <a name="input_rg_avdi"></a> [rg\_avdi](#input\_rg\_avdi)                                                         | Name of the Resource group in which to deploy avd service objects         | `string`       | n/a     |   yes    |
| <a name="input_rg_fslogix"></a> [rg\_fslogix](#input\_rg\_fslogix)                                                | Resource group FSLogix VM                                                 | `any`          | n/a     |   yes    |
| <a name="input_rg_image_name"></a> [rg\_image\_name](#input\_rg\_image\_name)                                     | Name of the Resource group in which to deploy image resources             | `string`       | n/a     |   yes    |
| <a name="input_rg_network"></a> [rg\_network](#input\_rg\_network)                                                | Name of the Resource group in which to deploy network resources           | `string`       | n/a     |   yes    |
| <a name="input_rg_pool"></a> [rg\_pool](#input\_rg\_pool)                                                         | Resource group AVD machines will be deployed to                           | `any`          | n/a     |   yes    |
| <a name="input_rg_shared_name"></a> [rg\_shared\_name](#input\_rg\_shared\_name)                                  | Name of the Resource group in which to deploy shared resources            | `string`       | n/a     |   yes    |
| <a name="input_rg_so"></a> [rg\_so](#input\_rg\_so)                                                               | Name of the Resource group in which to deploy service objects             | `string`       | n/a     |   yes    |
| <a name="input_rg_stor"></a> [rg\_stor](#input\_rg\_stor)                                                         | Name of the Resource group in which to deploy storage                     | `string`       | n/a     |   yes    |
| <a name="input_rt"></a> [rt](#input\_rt)                                                                          | Name of the route table                                                   | `string`       | n/a     |   yes    |
| <a name="input_scplan"></a> [scplan](#input\_scplan)                                                              | Name of the session host scaling plan                                     | `string`       | n/a     |   yes    |
| <a name="input_snet"></a> [snet](#input\_snet)                                                                    | Name of subnet                                                            | `string`       | n/a     |   yes    |
| <a name="input_spoke_subscription_id"></a> [spoke\_subscription\_id](#input\_spoke\_subscription\_id)             | Spoke Subscription id                                                     | `string`       | n/a     |   yes    |
| <a name="input_subnet_range"></a> [subnet\_range](#input\_subnet\_range)                                          | Address range for session host subnet                                     | `list(string)` | n/a     |   yes    |
| <a name="input_vm_size"></a> [vm\_size](#input\_vm\_size)                                                         | Size of the machine to deploy                                             | `any`          | n/a     |   yes    |
| <a name="input_vnet"></a> [vnet](#input\_vnet)                                                                    | Name of avd vnet                                                          | `string`       | n/a     |   yes    |
| <a name="input_vnet_range"></a> [vnet\_range](#input\_vnet\_range)                                                | Address range for deployment VNet                                         | `list(string)` | n/a     |   yes    |
| <a name="input_workspace"></a> [workspace](#input\_workspace)                                                     | Name of the Azure Virtual Desktop workspace                               | `string`       | n/a     |   yes    |

## Outputs

| Name                                                                                                                                                                               | Description                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| <a name="output_AVD_user_groupname"></a> [AVD\_user\_groupname](#output\_AVD\_user\_groupname)                                                                                     | Azure Active Directory Group for AVD users                 |
| <a name="output_azure_virtual_desktop_compute_resource_group"></a> [azure\_virtual\_desktop\_compute\_resource\_group](#output\_azure\_virtual\_desktop\_compute\_resource\_group) | Name of the Resource group in which to deploy session host |
| <a name="output_azure_virtual_desktop_host_pool"></a> [azure\_virtual\_desktop\_host\_pool](#output\_azure\_virtual\_desktop\_host\_pool)                                          | Name of the Azure Virtual Desktop host pool                |
| <a name="output_azurerm_virtual_desktop_application_group"></a> [azurerm\_virtual\_desktop\_application\_group](#output\_azurerm\_virtual\_desktop\_application\_group)            | Name of the Azure Virtual Desktop DAG                      |
| <a name="output_azurerm_virtual_desktop_workspace"></a> [azurerm\_virtual\_desktop\_workspace](#output\_azurerm\_virtual\_desktop\_workspace)                                      | Name of the Azure Virtual Desktop workspace                |
| <a name="output_dnsservers"></a> [dnsservers](#output\_dnsservers)                                                                                                                 | Custom DNS configuration                                   |
| <a name="output_location"></a> [location](#output\_location)                                                                                                                       | The Azure region                                           |
| <a name="output_session_host_count"></a> [session\_host\_count](#output\_session\_host\_count)                                                                                     | The number of VMs created                                  |
| <a name="output_vnetrange"></a> [vnetrange](#output\_vnetrange)                                                                                                                    | Address range for deployment vnet                          |
<!-- END_TF_DOCS -->
