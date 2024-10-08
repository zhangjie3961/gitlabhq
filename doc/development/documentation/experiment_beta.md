---
info: For assistance with this Style Guide page, see https://handbook.gitlab.com/handbook/product/ux/technical-writing/#assignments-to-other-projects-and-subjects
stage: none
group: unassigned
---

# Documenting experimental and beta features

Some features are not generally available and are instead considered
[experimental or beta](../../policy/experiment-beta-support.md).

When you document a feature in one of these three statuses:

- Add the tier badge after the page or topic title.
- Do not include `(Experiment)` or `(Beta)` in the left nav.
- Ensure the history lists the feature's status.

These features are usually behind a feature flag, which follow [these documentation guidelines](feature_flags.md).

If you add details of how users should enroll, or how to contact the team with issues,
the `FLAG:` note should be above these details.

For example:

```markdown
## Great new feature

DETAILS:
**Status:** Experiment

> - [Introduced](https://issue-link) in GitLab 15.10. This feature is an [experiment](<link_to>/policy/experiment-beta-support.md).

FLAG:
The availability of this feature is controlled by a feature flag.
For more information, see the history.
This feature is available for testing, but not ready for production use.

Use this new feature when you need to do this new thing.

This feature is an [experiment](<link_to>/policy/experiment-beta-support.md). To join
the list of users testing this feature, do this thing. If you find a bug,
[open an issue](https://link).
```

## When features become generally available

When the feature changes from experiment or beta to generally available, remove:

- The **Status** from the availability details.
- Any language about the feature not being ready for production in the body
  description.
- The feature flag information if available.

Ensure the history is up-to-date by adding a note about the production release.

## GitLab Duo features

Follow these guidelines when you document GitLab Duo features.

NOTE:
As of August, 2024, all GitLab Duo features except Code Suggestions have forward-looking tier statements, for example,
`For a limited time, Premium. In the future, Premium with GitLab Duo Pro.`
Use these type of statements until further notice.

### Experiment

When documenting a GitLab Duo experiment:

- On the [top-level GitLab Duo page](../../user/gitlab_duo/index.md), add a topic to the
 `Experimental features` section.
- Document the feature on the [GitLab Duo experiments page](../../user/gitlab_duo/experiments.md).
- Make sure you add history and status values, including any
  [add-on information](styleguide/availability_details.md#gitlab-duo-pro-or-enterprise-add-on).

### Beta

When a GitLab Duo experiment moves to beta:

- On the [top-level GitLab Duo page](../../user/gitlab_duo/index.md), move the topic from the
 `Experimental features` to the `Beta features` section.
- If the feature is documented on the [GitLab Duo experiments page](../../user/gitlab_duo/experiments.md),
  move the content somewhere more appropriate (near other related features).
- Make sure you update the history and status values, including any
  [add-on information](styleguide/availability_details.md#gitlab-duo-pro-or-enterprise-add-on).

### Generally available

When a GitLab Duo feature becomes generally available:

- On the [top-level GitLab Duo page](../../user/gitlab_duo/index.md), move the topic from the
 `Beta features` or `Experimental features` section to the `Generally available features` section.
- If the feature is documented on the [GitLab Duo experiments page](../../user/gitlab_duo/experiments.md),
  move the content somewhere more appropriate (near other related features).
- Make sure you update the history and status values, including any
  [add-on information](styleguide/availability_details.md#gitlab-duo-pro-or-enterprise-add-on).
