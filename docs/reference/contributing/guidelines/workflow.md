### Workflow

#### Gatekeepers

##### Mbed OS maintainers

The maintainers are a small group of Mbed OS engineers who are responsible for the Mbed OS codebase. Their primary role is to progress contributions, both internal and external, from the initial pull request state through to released code. 

Responsibilities:

1. Check for CLA (Contributor License Agreement) compliance.
1. Ensure the relevant stakeholders review pull requests.
1. Guide contributors both technically and procedurally.
1. Run pull requests through the CI systems.
1. Put label version.
1. Merge pull requests into the requested branches.
1. Make periodic patch and feature releases.

The current maintainers are:

* Anna Bridge (adbridge).
* Martin Kojtal (0xc0170).
* Jimmy Brisson (theotherjimmy).
* Shrikant Tudavekar (studavekar).
* Sam Grove (sg-).
* Cruz Monrreal (cmonr).

##### Stakeholders

They are responsible for a specific mbed OS module or feature.

Responsibilities:

1. Review pull request and coordinate reviews within the team
1. Ensure the version label is correct

#### Contributions

All code changes and additions to Mbed OS are handled through GitHub. If you want to contribute, either by adding features or by fixing bugs, please follow the guidelines for [new features](#contributing-new-features-to-mbed-os) and [bugs](#reporting-and-fixing-bugs). In both cases, please follow the [code style guide and GitHub pull request guidelines](/docs/v5.7/reference/guidelines.html#style)</a>. Please also read the [CLA](/docs/v5.7/reference/guidelines.html#cla) guidelines because we will immediately close pull requests submitted without a CLA.

Before contributing an enhancement (new feature, new port and so on), please [discuss it on the forums](https://os.mbed.com/forum/bugs-suggestions/) to avoid duplication of work, as we or others might be working on a related feature.

Patch contributions can only be accepted through GitHub by creating a pull request from forked versions of our repositories. This allows us to review the contributions in a user friendly and reliable way, under public scrutiny.

Please create separate pull requests for each concern; each pull request should have a clear unity of purpose. In particular, separate code formatting and style changes from functional changes. This makes each patch’s true contribution clearer and therefore quicker and easier to review.

##### Reporting bugs

Before submitting a bug report or a bug fix, please [discuss it on the forums](https://os.mbed.com/forum/bugs-suggestions/) to avoid duplication of work, as we or others might be working on it already.

The bug report requires a clear instructions how to reproduce it - describe everything in detail. Insufficient bug reports will be closed.

All Mbed OS is on GitHub; please use GitHub's [issues mechanism](https://guides.github.com/features/issues/) to open a bug report directly against the relevant GitHub repository.

#### Guidelines for GitHub pull requests

Pull requests on GitHub have to meet the following requirements to keep the code and commit history clean:

- Commits should always contain a proper description of their content. Start with a concise and sensible one-line description. Then, elaborate on reasoning of the choices made, descriptions for reviewers and other information that might otherwise be lost.
- You should always write commits to allow publication, so they can never contain confidential information, reference private documents, links to intranet locations or rude language.
- Each commit should be the minimum self-contained commit for a change. A commit should always result in a new state that is again in a compilable state. You should (if possible) split large changes into logical smaller commits that help reviewers follow the reasoning behind the full change.
- Commits should follow [Chris Beam’s seven rules of great commit messages](http://chris.beams.io/posts/git-commit#seven-rules):
	1. Separate subject from body with a blank line.
	1. Limit the subject line to 72 characters (note that this is a deviation from Beam's standard).
	1. Capitalize the subject line.
	1. Do not end the subject line with a period.
	1. Use the imperative mood in the subject line.
	1. Wrap the body at 72 characters.
	1. Use the body to explain _what_ and _why_ vs _how_.
- Because we use GitHub and explicit CLAs, special commit tags that other projects may use, such as “Reviewed-by”, or “Signed-off-by”, are redundant and should be omitted. GitHub tracks who reviewed what and when, and our stack of signed CLAs shows us who has agreed to our development contribution agreement.
- Prefixing your commit message with a domain is acceptable, and we recommend doing so when it makes sense. However, prefixing one's domain with the name of the repo is not useful. For example, making a commit entitled "mbed-drivers: Fix doppelwidget frobulation" to the `mbed-drivers` repo is not acceptable because it is already understood that the commit applies to `mbed-drivers`. Renaming the commit to "doppelwidget: Fix frobulation" would be better, if we presume that "doppelwidget" is a meaningful domain for changes, because it communicates that the change applies to the doppelwidget area of `mbed-drivers`.
- All new features and enhancements require documentation, tests and user guides for us to accept them. Please link each pull request to all relevant documentation and testing pull requests.
- Avoid merging commmits (always rebase when possible).
- Pull requests shall fix a bug or add a feature or refactor.

#### Pull request categories

##### Bugfixes

The last line in your commit message description should say “Fixes #deadbeef”, where “deadbeef” is the issue number in GitHub. This allows GitHub to automatically close the issue when the commit is merged into the default branch.

Every bugfix should contain a test to verify results prior and after the pull request.

##### Changes/additions

Backward compatible changes (refactoring, enhancements) or new target additions are considered to be part of the patch release.

##### Features

New features should initially be implemented on a separate branch in the Mbed OS repository. The naming convention for a feature branch is: "feature-".

Each feature has a tech lead. This person is responsible for:

- rebasing often to track master development
- reviewing any addition to the feature branch (approval required by the feature owner or a person assigned to do instead)

#### GitHub pull requests workflow

Each pull request goes through the following workflow:

<span class="images">![](https://s3-us-west-2.amazonaws.com/mbed-os-docs-images/Workflow.png)<span>The workflow of merging a pull request</span></span>

#### Pull request states

Labels that the Mbed OS maintainers add to a pull request represent the pull request workflow states. The Mbed OS maintainers are responsible for moving pull requests through the workflow states.

Each state is time boxed. In most cases, this should be sufficient time to move to an another state.

##### Reviews

All pull requests must be reviewed. The mbed CI bot determines the most suitable person to review the pull request and tags that person accordingly.

Time: 3 days for reviewers to leave feedback since the label was added

##### The CI (Continuous Integration) testing

There are a number of CI systems available. Which CI tests we run against a particular pull request depends on the effect of that pull request to the code base. Irrespective of which CIs tests run, Mbed OS has an all green policy, meaning that all the CI jobs that are triggered must pass before we merge the pull request.

Time: 1 day for CI to complete and report back results

The CI workflow can be found [here](tbd)

##### Work needed

The pull request requires additional work due to failed tests, changes requested.

Time: 3 days to respond to the review comments

##### Releases

Once we merge a pull request, we tag it with a release (not applicable for feature pull requests). This is the release in which we first publish this pull request. For patch releases, we allow only bug fixes, new targets and enhancements to existing functionality. New features only go to feature releases.

The release tag has the following format:

*release-version: 5.f.p* - Where `f` is the feature release and `p` the patch release.

#### Additional labels

We use many other labels to summarize the scope and effect of the changes.

- *needs: preceding PR* - This pull request cannot yet be merged because it has a dependency on another pull request that needs to merge first.
- *DO NOT MERGE* - This pull request contains changes that may be in a draft state and submitted purely for review, or may contain breaking changes that have not been considered.
- *devices: 'name'* - The pull request specifically affects the named device(s).
- *component: 'name'* - The pull request specifically affects the named component.

The following labels summarize the scope of the pull request.

- *scope: bug-fix*.
- *scope: feature*.
- *scope: new-target*.
