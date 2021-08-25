---
layout: page
title: How We Do It
permalink: /publishing/how_we_do_it
---

# Why Share?
It's true that we don't need to be sharing the what/why/how of what we do, but we're big proponents of supporting the broader open-source community.  Who knows, maybe you'll find a useful nugget that might help you in your journey.  We hope so!

# Useful GitHub Actions
Here are the community-developed GitHub Actions that we use:

* [mshick/add-pr-comment](https://github.com/mshick/add-pr-comment)

  This is used pretty heavily to post comments to a PR.  Useful for providing feedback to the PR.

* [cla-assistant/github-action](https://github.com/cla-assistant/github-action)

  This is a terrific way of making sure folks agree to a Contributor License Agreement (CLA).  It's non-intrusive, easy-to-use/follow and very simple to deploy.

* [SonarSource/sonarcloud-github-action](https://github.com/SonarSource/sonarcloud-github-action)

  Pretty self-explanatory, but this is for SonarCloud.io automatic scanning.

# Other Tools

#### RepoLinter
[RepoLinter](https://github.com/todogroup/repolinter) is totally awesome.  It allows for easy scanning of the repo and is *really* useful.  Unfortunately there's no officially-supported Docker image for it, so we built our own and published it privately to our GitHub Container Registry.  Not ideal, but we're not in the business of building/hosting RepoLinter containers, so decided this was probably best.  For some reason it didn't build out-of-the-box, but did after modifying `Dockerfile` a bit along with a `run_repolinter.sh` script.

#### Scancode-Toolkit
[Scancode-Toolkit](https://github.com/nexB/scancode-toolkit) is a terrific tool for detecting the license(s) used.  We use for this purpose.  Incidentally, it's another great tool that we had to build (and host, privately) the container for.  It would be great if there was a ready-to-go (officially supported) container, but none was available.  Certainly not capping on this project, as it's super useful... just deploying it was a bit more involved because of the lack of a publicly available "official" container.
