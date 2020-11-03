---
title: "Release Resources and Template"
---

*Releases* are the mechanism for packaging a set of features, bug fixes, and other modifications to a software repository. This page provides information about compiling (tagging) a release and its release notes, as well as examples and other web resources on this topic.

## Tagging a Release

GitHub releases are driven by version tags (e.g., v1.0) applied to a set of commits.

1. View a log of your commit history. Ex: `$ git log` or `$ git log --pretty=oneline`
2. Decide which commits to include in the release.
3. Apply the version tag to the last (most recent) commit's checksum. Ex: `$ git tag -a v1.0 4c73e1`
    * This action will prompt you to enter a message corresponding to the tag. Ex: `News templates`
4. Confirm the commit tagged for the release. Ex: `$ git show v1.0`
5. Push tag(s) to `origin` or `upstream` as appropriate. Ex: `$ git push origin v1.0` or `$ git push origin --tags`
6. View your releases under your repo's Code tab, which lets you toggle between Releases and Tags. This is where the message from step 3 appears. Ex: [this repo](https://github.com/LLNL/.github/releases)

## Writing Release Notes

GitHub allows you to [draft release notes directly in the UI](https://help.github.com/en/github/administering-a-repository/managing-releases-in-a-repository). The steps are straightforward:

1. Start a new draft release.
2. Define its corresponding version (tag) number and branch.
3. Give the release a title and description.
4. Publish the release. Ex: [this repo v1.1](https://github.com/LLNL/.github/releases/tag/v1.1)

*Note:* Be as clear as possible in your release notes so users know what they're getting. Ideally, this means each commit message is unique and direct. You may also want to organize your notes into categories such as Enhancements, Bug Fixes, Deletions, etc. to help users navigate a long list of changes or highly detailed notes.

## Resources

* Start here: [Releasing projects on GitHub](https://help.github.com/en/github/administering-a-repository/releasing-projects-on-github)
* [About releases](https://help.github.com/en/github/administering-a-repository/about-releases)
* Basic: [Managing releases in a repository](https://help.github.com/en/github/administering-a-repository/managing-releases-in-a-repository)
* Advanced: [Automation for release forms with query parameters](https://help.github.com/en/github/administering-a-repository/automation-for-release-forms-with-query-parameters)
* [Git tagging basics](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
