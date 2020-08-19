# Higher Order Scaffolders

Start Date: 2020-08-16

Author: @travi

## Summary

Define a pattern for scaffolders that can follow a more rigid process than
simple plugins, like package or application scaffolders. Because they solve a
well defined problem, they are able to define answers to the generic questions
provided by default in the [project-scaffolder](https://github.com/travi/project-scaffolder)
or language scaffolders. These also need to define details commonly returned as
results from the plugin/sub-scaffolders, like `dependencies`,
`devDependencies`, `scripts`, and others.

## Motivation

* Further automate well-defined scenarios that have become repetitive
* Enable orchestrating project scaffolding tasks at a higher level so that
  larger tasks can be automated, like creating the initial projects to
  bootstrap a new organization.

## Detailed Explanation

Scaffolding some projects can be detailed enough to know the decisions that
should be made related to the generic project prompts. With the current
approach to enabling scaffolding of specific package/application projects
through plugins, there is no way for the plugin to provide these decisions to
the scaffolding workflow.

The primary decision here is to enable decisions to be provided programatically
while continuing to enable the behaviors available to plugins.

## Rationale and Alternatives

{{Discuss 2-3 different alternative solutions that were considered. This is
required, even if it seems like a stretch. Then explain why this is the best
choice out of available ones.}}

* Continue to build package/application plugins and manually answer prompts,
  even if they are repetitive and error prone

## Implementation

{{Give a high-level overview of implementation requirements and concerns. Be
specific about areas of code that need to change, and what their potential
effects are. Discuss which repositories and sub-components will be affected, and
what its overall code effect might be.}}

{{THIS SECTION IS REQUIRED FOR RATIFICATION -- you can skip it if you don't know
the technical details when first submitting the proposal, but it must be there
before it's accepted}}

## Unresolved Questions and Bikeshedding

{{Write about any arbitrary decisions that need to be made (syntax, colors,
formatting, minor UX decisions), and any questions for the proposal that have
not been answered.}}

* if we go the route of calling `project-scaffolder` within these, what should
  the object be named that provides the details normally found in `results`?
* higher-order scaffolder doesnt actually seem like an appropriate name for
  this. what would be more accurate? maybe i'm thinking more "high-level" than
  "higher-order"
* should the approach to package/application plugins be reconsidered if this
  approach is available?

{{THIS SECTION SHOULD BE REMOVED BEFORE RATIFICATION}}
