# Azure Remediation Policies
This repository contains Azure policy definitions that can be used for auto remediating the non-compliant resources. These policies are also used along with the Cloudneeti auto-remediation feature.

## How to Use 
This repository contains Azure policy definitions with *DeployIfNotExists* (DINE) effect. These policies help to remediate the non-compliant resources present in Azure. DINE policies automatically remediate the new resources which are without required configuration. These policies also used to remediate the existing resources with the help of remediation tasks.

We have categorized the remediation policies on the basis of Azure services. To use specific remediation policy on the subscription, Go to the individual policy directory and run the below commands,

1. Login to Azure Account

    ````powershell
    Connect-AzAccount -Subscription <SubscriptionId>
    ````

2. Create Policy Definition

    ````powershell
    $definition = New-AzPolicyDefinition -Name <PolicyName> `
                                         -DisplayName <DisplayName> `
                                         -Description <description> `
                                         -Policy '.\azurepolicy.rules.json' `
                                         -Parameter '.\azurepolicy.parameters.json' `
                                         -Mode <All/Indexed>
    ````
    While creating the policy definition use *metadata.json* file for the Name, DisplayName, Description and Mode parameters.

2. Create Policy Assignment
    ````powershell
    $assignment = New-AzPolicyAssignment -Name <assignmentname> -Scope <scope> -PolicyDefinition $definition
    ````
    Here, scope can be at management group level, subscription, resource group or resource level.

Refer [Resources/References](##Resources/References) section to understand the Azure Policy framework and its working.


## Create policy Definitions (to use with Cloudneeti Remediation)
Follow below steps to create policy definitions inside Azure subscription

1. Clone Azure Remediation Policy repository

	`# git clone https://github.com/Cloudneeti/azure-remediation-policy.git`

3. Change to remediation directory

	`# cd azure-remediation-policy`

3. Provision policy definition in the subscription

	 `# .\provision-PolicyDefinitions.ps1 -SubscriptionId <Subscription Id>`
	 
	 **Note:** Run `cd $user` to switch user directory before executing above command if you are using CloudShell
	 

TODO: Create policy definitions at the Azure management group level, so that they can be shared across multiple subscriptions.

## Remediation Policies Supported
Refer [here](remediation-policies.md) for list of available remediation policies

## Contribute

## Resources/References
* [Azure Policy Overview](https://docs.microsoft.com/en-us/azure/governance/policy/overview)
* [Understand Policy Effects](https://docs.microsoft.com/en-us/azure/governance/policy/overview)
* [Programmatically Create Policies](https://docs.microsoft.com/en-us/azure/governance/policy/how-to/programmatically-create)
* [Get Compliance Data](https://docs.microsoft.com/en-us/azure/governance/policy/how-to/get-compliance-data) 
* [Remediate non-compliant Resources](https://docs.microsoft.com/en-us/azure/governance/policy/how-to/remediate-resources)

## Disclaimer

Copyright (c) Cloudneeti - All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND ONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
