---
layout: page
title: Standards
permalink: /publishing/standards
---

# Repository Naming
Although our repo names vary a bit, we do have a rhyme and reason with how we name repos.  Here goes!

| Type of Content | Naming Standard | Notes |
|-----------------|-----------------|-------|
| Terraform Modules | `terraform-oci-<name>` | This format is needed for publishing to the [HashiCorp Terraform Module Registry](https://registry.terraform.io/browse/modules). |
| DevO Content | `devo-<name>` | This is for text-based content that is going to DevO. |
| Language-specific solution | `<language>-<name>` | To keep it somewhat organized, we try to group by language for many projects.  Names such as `go-hello-world`, `ruby-hello-world`, etc. are just a few ideas.  Clearly we're looking for more than `hello-world` projects, but you get the idea!  ;)
| Tool | `<name>` | There are some projects that are tools.  While they *could* go under the language-specific definition above, they typically have a really cool name that we just don't feel right ruining with a language-specific prefix.  This is a bit subjective, but if there's a really cool name for something, we want to keep a good thing going! |

# Required Repo Structure
We try to focus on being flexible and easy-to-use.  There is a minimum set of files and structure that we do enforce (via Actions).  Rather than just surprise you, here's what we expect (at minimum):

```
.
├── .github
├── .gitignore
├── LICENSE
└── README.md
```

## .gitignore
We expect the `.gitignore` file to ignore superfluous and extraneous "clutter" that's not necessary (things like hidden files that are not really needed, local caching files, etc.).  You'll likely need to adjust the `.github` file for the language(s) and framework(s) you'll be using in your project.  Customize away!

# Branching
We do not enforce a specific branching strategy, but leave it up to each project maintainer to dictate what's best for the project.  See [Working With Our Repos](/publishing/working_with_repos) for more info.

# Commit/PR Comments
We prefer to standardize on using [ConventionalCommits](https://www.conventionalcommits.org/en/v1.0.0/) when generating change logs and creating comments on commits, PRs, etc.

# Scanning of Source Code
Most projects that contain source code (all but the text-only repos) are setup to be scanned by SonarCloud.io, along with a scanning status badge on the README.  Feel free to use (leave) this badge in-tact, as it's a nice marker to instill confidence in your code (or to encourage you to improve it).

# Committing Code
Do not commit directly to `main`.  It won't work anyway (`main` is protected).  Use Pull Requests (PRs) instead.  You can do this via a fork or branch.  If you're a maintainer, you can create a branch (you have permissions to do so).  If you're an outside contributor (or maintainer), you may fork the project (you don't have permissions to create a branch in the repo).  See [Working With Our Repos](/publishing/working_with_repos) for more info.

<br><br>
[< What's Expected of You](/publishing/expectations) \| [Getting a Repository >](/publishing/getting_a_repo)
