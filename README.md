# tfc-sentinel
TFC Sentinel tests

Not a full-blown repo, follow-along tehn Sentinel Guide from : https://learn.hashicorp.com/terraform/sentinel/sentinel-intro

# How-To

## What is it ? 
Sentinel is a paid feature of Terraform Cloud. The integrated Sentinel language and policy framework is embedded into Terraform Cloud to enable fine-grained, logic-based policy decisions. A Sentinel Policy is a guard-rail for Terraform deployments and defines the circumstances which certain behaviors are allowed.

Sentinel can also use external information for policy decisions with imports from other resources.

Sentinel also allows cost-centric policies to be created and then automatically enforced in the Terraform workflow. 

## Some takes 

Sentinel enables:

- *Fine-Grained Policy*: Most ACL systems only enable coarse-grained behaviors: "read", "write", etc. Sentinel enables fine-grained behavior such as disallowing a certain API call when specific parameters are present.

- *Logic-Based Policy*: You can write policy using full conditional logic. For example, you may only allow a certain application behavior on Monday to Thursday unless there is a manager override.

- *Enforcement levels*: Sentinel allows policies to be defined along with an "enforcement level" that dictates the pass/fail behavior of a policy. Advisory policies warn if they fail, soft mandatory policies can have their failures overridden, and hard mandatory policies must pass under all circumstances. Having this as a built-in concept enables you to model policy more accurately and completely for your organization.


## Get simulator

Policies are verified with the Sentinel Simulator tool, which can be downloaded here : https://docs.hashicorp.com/sentinel/downloads



