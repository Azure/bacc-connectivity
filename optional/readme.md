# Currently Working On 


- Define VPN p2s connection with certifcate



- Design Question: How to allow flexibility in not deploying JumpBox, VpnGw, AzFw but keep the configurations for UDR, NSG etc in the config file?

- Optional Folder: In case we need a ready to be used spoke vnet w/o Azure Batch configuration


# Already Deployed: 

- Resource Groups
- NSGs, Routes
- VNet and Subnets
- Log Analytics Workspace
- Application Insights
- pip AzFirewall
- Azure Firewall
- pipBastion
- Azure Bastion
- VPN Gateway depoloyment
- Create public IP for VPN Gateway (like for AzFW and Bastion, so we can have the same naming convention) - done?
- private DNS Zone (link to Hub Vnet)
- Linux VM Jumpbox
- Windows VM Jumpbox
- Verify if Workspace ID is enabled on all resources
- Propagate diagonstic settings
- Use diagnostic.json config file
- Custom Script for Linux Jumpbox not executed? -> possibly wrong datatype for custom data (string expected, not base64) -> solved.
- 'AzureAsyncOperationWaiting' errors when Bastion and FW are both set to false - only VPNG to true -> solved
- Solved: if AzFW true and Bastion True, but VPNGW false -> concurracy issue on Gateway Subnet -> error. Not clear, what causes the concurracy race: stopped after both (L,W) Jumpboxes were commented out.... added azFw and azBastion to dependencies
- Collect all relevant output for Secure Batch Repository (as input)
- VM Jumpboxes: Win (for Win: can we use a an image version which supports VTMP module?)
- Initial Cleanup / Cleanup dependencies on other resources after code fix
- Design Decision: Always create all subnets, nsgs and routes, so no status is needed in config file
- Deployed: dns resolver to allow private endpoint resolution when using p2s vpn connectivity. 
- VPN Gateway and private IP resolution - works with conditonal forwarding (tested on MAC OS)
- Need to agree how to deal with security constratints, like storage account access: only allow from certain VNETS or add (on-prem) local IP  to list of allowed storage accounts?

# Open

- Create a Spoke Network incl. subnets and peering to Hub + link to private DNS? (AzBatch side)

- Review applicationRuleCollection in Azure Firewall
- Review networkRuleCollection for Spoke to Spoke connectivity

- Implement schema validation?
- GitHub Auto-Testing

# Nice to Have: 


- VM Jumpbox: Can we apply a DSC config? -> allow RDP to Windows Images (in case we want to domain join them)

# Known Issues 

to feedback to Libs Team:

-> might be related to LibModule for VNets -> added batchsize(1) annotation to force the for loop to execute 1 subnet at the time
-> file PR for custom extension: CodeToExecute was not part of the final parameter set.