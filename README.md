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


## Walk-through

Check : 
```go
hour = 4
main = rule { hour >= 0 and hour < 12 }
```

This first line of this example declares a variable named hour with the value 4. The second line declares a rule that will return true if hour is between 0 and 12.

This policy can be applied using Sentinel Simulator to determine whether this policy passed or failed. Save this file as [policy.sentinel](policy.sentinel) and run the Sentinel Simulator against it : 
```bash
sentinel apply policy.sentinel
Pass
```
This example introduces a core concept of Sentinel; Rules. Rules are the primary definitions within a policy. Rules are boolean operators that evaluate whether a statement is true or false. The result of a rule can be used to determine whether or not a Terraform action can execute. We'll look more at rules and how they function.

### Rules

All policies need a main rule. This is the rule that that defines the final output of Pass or Fail in Sentinel. Let's take a look at more complex rule:

```go
import "tfplan"

main = rule {
  all tfplan.resources.aws_instance as _, instances {
    all instances as _, r {
      r.applied.tags else null is not null
      }
  }
}
```
??? what is this ?? `r.applied.tags else null is not null`  - makes no sense for me so far