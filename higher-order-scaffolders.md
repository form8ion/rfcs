# High-Level Scaffolders

Start Date: 2020-08-16

Author: @travi

## Summary

Define a pattern for scaffolders to enable full orchestration of the
scaffolding process. While some cases may still leave a few choices open to the
user, it should be possible to programatically provide decisions to all
prompts. Because mechanisms already exist to execute scaffolding tasks like
defining dependencies, scripts, and other standard steps, it is unnecessary to
duplicate that functionality. However, plugins can be provided for these
existing mechanisms, which can then be programatically executed.

## Motivation

* Further automate well-defined scenarios that have become repetitive, like
  extending shareable ESLint configs or babel presets
* Enable orchestrating project scaffolding tasks at a higher level so that
  larger tasks can be automated, like creating the initial projects to
  bootstrap a new organization.

## Detailed Explanation

Scaffolding some projects can be detailed enough to know the decisions that
should be made related to the generic project prompts. With the current
approach to enabling scaffolding of specific package/application projects
through plugins, there is no way for the plugin to provide these decisions to
the overall scaffolding workflow.

The primary goal here is to enable decisions to be provided programatically
that allow more detailed orchestration of the scaffolding process.

## Rationale and Alternatives

### Alternatives

* Continue to build package/application plugins and manually answer prompts,
  even if they are repetitive and error prone. This is essentially where the
  state of the scaffolding suite currently is. There are repetative tasks that
  I already find myself avoiding because they are tedious, but with very well
  defined steps that need to be repeated.
* adjust the flow of scaffolding to follow chain-of-responsibility or similar
  so that the input and output interfaces align and could be executed in any
  order. this is along the lines of [how enhancers are applied](https://github.com/form8ion/lift/blob/master/src/enhancers.js?rgh-link-date=2020-08-19T05%3A50%3A03Z)
  in [lift](https://github.com/form8ion/lift). however, making a change like
  this would be a major redesign of how the scaffolder suite works. while there
  could value in interating in this direction, it seems out of scope for the
  goal of high-level scaffolding. if we do make changes like this, it should
  be a separate effort, with this goal met afterward within that new context.

### Rationale for high-level scaffolder approach being the best

Limiting the changes necessary for enabling the desired high-level orchestration
to essentially calling the [project-scaffolder](https://github.com/travi/project-scaffolder)
with specific decisions accomplishes the goal with minimal redesign of
the overall flow. Existing capabilities from plugins are still enabled, but
exposed to the high-level scaffolder through the ability to define decisions
that result in executing the specific plugins.

## Implementation

The high-level will call the [project-scaffolder](https://github.com/travi/project-scaffolder),
passing the options that would normally be passed directly to the [project-scaffolder](https://github.com/travi/project-scaffolder),
but enhanced with `decisions` that define the desired flow to accomplish the
goals of the high-level scaffolder.

For now, the high-level scaffolders will not be managed by another tool, but
expected to be called directly by consumers. This will likely be a matter of
calling the high-level scaffolder(s) directly from a sub-command of a cli. This
could be a separate sub-command for each high-level scaffolder, but may be
simpler as a chooser in an existing `scaffold` command, as a peer to executing
the generic flow.

While I'm not yet ready to build such a tool, this approach will also enable
execution from a tool that calls multiple high-level scaffolders in a single
command.

There are likely still a handful of paths that need `decisions` to be passed to
them, like [the package-type plugins](https://github.com/travi/javascript-scaffolder/blob/9eadb5f9134bf01763376a71a2357e5a5fe1e64f/src/project-type/package/scaffolder.js#L93).

## Unresolved Questions and Bikeshedding

{{Write about any arbitrary decisions that need to be made (syntax, colors,
formatting, minor UX decisions), and any questions for the proposal that have
not been answered.}}

* what should the convention be for the named export from packages that define
  a high-level scaffolder? language scaffolders and plugins export `scaffold`
  by convention. we would want something similar for this that is exported
  consistently for high-level scaffolders

{{THIS SECTION SHOULD BE REMOVED BEFORE RATIFICATION}}
