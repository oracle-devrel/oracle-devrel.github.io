# Working With Our Repositories
## Submitting Code
The `main` branch is protected and requires a pull request (PR) to merge code (pushing directly to `main` will fail).  A pull request to `main` requires at least one review before it can be merged.  There are a couple of ways to do this:

* Fork the repo, push changes and then submit a PR
* Create a branch, push changes to the branch and then submit a PR

Either of the above options will require you to receive at least one review (approving the PR) before your code can be merged.

## Change Log and Comment Format
We prefer to standardize on using [ConventionalCommits](https://www.conventionalcommits.org/en/v1.0.0/) when generating change logs and creating comments on commits, PRs, etc.

## Branches
There are lots of branching strategies out there.  We don't dictate how to use branches, but leave this up to the project/repo maintainer(s) to decide how to use branches.  Each maintainer is able to select a branching strategy that they're most comfortable with.

## Automated Checks
There are several checks which are setup by default.  These checks must successfully pass before a merge can be made.  Your repo will be setup to pass the checks.

Here's what's needed to pass:

* Make sure to only use pre-approved licenses

    You may use other licenses, however until the project (repo) has been approved to use a non-pre-approved license, you will not be able to merge the PR (that's failing the license validation check).

* Include the proper copyright notice on the **first line**

    Make sure that the following code is present: `Copyright (c) 2021 Oracle and/or its affiliates.`  It's also ok to use something like ``Copyright (c) 2000-2021 Oracle and/or its affiliates.` (a range of years, instead of a single year).  Both will pass just fine.  If this is missing, warnings will be raised and a comment made on the PR (notifying you of which file(s) is missing the copyright notice).

## Forbidden File Changes
There are several files and/or directories that should not be modified (are prohibited from being modified):

* `.github`
  
    The `.github` directory (and all of its contents) are by default blocked.  This is to maintain the integrity of the automated pipelines (dependent on GitHub Actions, which are defined in the `.github` directory).
  
* `repolinter.json`
  
    This is used to define what Repolinter is examining.  It's referenced by the automated pipeline, so is protected from modification.

* `license_policy.yml`
  
    Used by Scancode-Toolkit, for license validation.  It's referenced by the automated pipeline, so is protected from modification.

* `sonar-project.properties`
  
    The config needed by SonarCloud integration.  It's referenced by the automated pipeline, so is protected from modification.

## Pre-Approved Licenses
Just like most companies, we pride ourselves in top-notch open-source.  One of the key areas is ensuring a license is used that aligns with the goal of the organization.  There are a plethora of different licenses out there... we're not going to argue that one is better than the other, however we have selected some that best align with our goals.

DRGHO repositories must align to using one (or more) of the pre-approved licenses.

Pre-approved licenses:

* Universal Permissive License (UPL) version 1.0

## Releases and Tags
Just like branches, we don't dictate how tags will be used or how you manage your releases.  We do suggest using (and standardize on, though we don't enforce it) using [Semantic Versioning](https://semver.org) for your versioning strategy.

When it comes to releases, we provide the ability to auto-generate (and upload) assets to the release.  Each time a release is *published*, an Action is triggered which will read the `release_files.json` file in the root of the repo.  This JSON file can specify one or more ZIP files to create and/or upload file(s) to the release.

### Sample Scenario
A common scenario is where a Terraform stack is created and published.  The desire is that a user cloning/downloading the repo will likely use it with [Terraform CLI](https://www.terraform.io) and/or [OCI Cloud Shell](https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/cloudshellintro.htm).  This requires modifying the `provider.tf` file (or whatever file your providers are defined in), creating a ZIP file and uploading the ZIP file to a release (this is the easiest way to distribute a stack for easy deployment).

Let's pretend that we have the following directory/file structure:

```
.
├── README.md
├── data_sources.tf
├── iam.tf
├── LICENSE
├── network.tf
├── ods.tf
├── orm
│   └── provider.tf
├── provider.tf
├── schema.yaml
├── services.tf
├── tags.tf
├── terraform.tfvars.template
└── variables.tf
```

The `./provider.tf` file is what is setup to be used by Terraform CL, while `./orm/provider.tf` is configured to be used by ORM.  Here's how we might build a ZIP file and upload it to any given release in our repo (this is all configured in `release_files.json` in the root of the repo):

```
[
  {
    "action": "create_zip",
    "file_name": "my-tf-stack-latest.zip",
    "files": [
      {
        "src_pattern": "*.tf",
        "exclude": [
          "provider.tf"
        ]
      },
      {
        "src": "LICENSE"
      },
      {
        "src": "schema.yaml",
      },
      {
        "src": "orm/provider.tf",
        "dst": "provider.tf"
      }
    ]
  },
  {
    "action": "upload_file",
    "file_name": "my-tf-stack-latest.zip"
  }
]
```

There are two actions:
1. Create the ZIP file
2. Upload the ZIP file (to a published release, which triggers the Action)

For creating the ZIP file, several source files are included:
* All `.tf` files (except `provider.tf` in the root, which is intended for Terraform CLI and wouldn't work with ORM)
* The `LICENSE` and `schema.yaml` files
* An ORM-specific `provider.tf` file (in the `orm` subdirectory)

There are a lot of other options available, so if you're curious or looking for more functionality, check out the documentation at [https://github.com/oracle-devrel/action-release-zip-maker](https://github.com/oracle-devrel/action-release-zip-maker).