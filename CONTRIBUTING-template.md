# Introduction

### HI THERE!

>First off, thank you for considering contributing to Crypto Done Right (CDR). Because of people like you that make CDR such a practical knowledge base.  Read the following sections in order to know how to ask questions and how to contribute to something.

### About CDR
> CDR is a new project and with the ever-changing and evolving field of cyber security and cryptography, we continues to actively invite maintainers and contributers.
> You can help out with cryptography practices that are used in all areas! There is plenty of work to do. But, no big commitment required.
> If all you do is review a single Pull Request, you are a maintainer! You become people's hero by keeping our content updated so people all around world can see and learn and we in turn can have have a better way to keep everyone's data safe and secure.

### Your First Contribution
There are so many ways to contribute!
- Create a [Pull Request](/pull_request_template.md).
- Review a [Pull Request](/pull_request_template.md).
- Fix an [Issue](/issue_template.md).
- [Share your thoughts with us](https://docs.google.com/forms/d/e/1FAIpQLSenaO1MbJ5sgjKF5KYp-AwMbLEsiuEEioqOUnI1dqvievTAKw/viewform).
- [Contact us!](/contact.html)

### Branches
Master Branch
> When contributors create a branch in their project, they are creating an environment where they can try out new ideas. Changes they make on a branch don't affect the master branch, so everyone is free to experiment and commit changes without worrying about making changes to the actual website. The changes are not deployed until they are reviewed in the Development Branch.

Development Branch
> This is where we can review content that has been contributed for final in production before merging to the master branch.
Once contributor’s  pull request has been reviewed and the branch passes the tests, we move the changes to the master branch to deploy them to the website. If our  branch causes issues, we  can roll it back by deploying the existing master into production.

### Templates
> You can open a PULL REQUEST at any point during the development process! If you're using a Fork & Pull Model,  Pull Requests provide a way to notify CDR maintainers about the changes you'd like them to consider. Our CDR Development Branch follows the Shared Repository Model,  Pull Requests help start code review and conversation about proposed changes before they're merged into the master branch.  Pull Requests initiate discussion about your commits. Because they're tightly integrated with the underlying Git repository, anyone can see exactly what changes would be merged if they accept your request.

> The ISSUE TEMPLATE is to help contributors open meaningful issues. Issues can also be assigned to other users and tagged with labels for quicker searching.
> With issues, you can also:
> - Associate issues with pull requests so that your issue automatically closes when you merge a pull request.
> - Transfer open issues to other repositories.
> - Pin important issues to make them easier to find, preventing duplicate issues and reducing noise.
> - Report comments that violate GitHub's Community Guidelines.


[Pull_request_template.md](/pull_request_template.md).

> This is the template we follow when we want to:
> - Code bug fix
> -  Current content fix (update outdated contents, error fix, proofreading, etc.)
> -  New content creation
> -  Website UI modifications
> -  Others (please specify)

[Issue_template.md](/issue_template.md).
> This is the template we follow for the following activities:
> -  Code Bug
> -  Error in Content
> -  Outdated Content
> -  Page Layout
> -  URL Linking Issue
> -  Other (please specify)

### About Jekyll
> We are currently using Jekyll to populate our static pages.

For general topic page, use the following to create the page
```
---
layout: page
title: sample
type: cryptographic_protocols
update: Last Updated Fri, 3 May 2019 19:37:01 -0400
permalink: "articles/cryptographic_protocols/test"
alerts:
  - id: 1
    type: success
    description: If this is a recommended protocol, you can put explaination here. If none, remove this id 1 section.
    link: "if there is a reference link, you can link it here."
  - id: 2
    type: warning
    description: If this must used with caution, put explaination for the warning here. If none, remove this id 2 section.
    link: "if there is a reference link, you can link it here."
  - id: 3
    type: danger
    description: If this is no longer a good practive, put danger warning here. If none, remove this id 3 section.
    link: "if there is a reference link, you can link it here."
further-reading:
  - name:sample
    link:
  - name:sample
    link:
attacks:
  - name: sample
    description: ": sample"
    link: ""
  - name: sample
    description: ": sample"
    link: ""

---
Contents go here!
```

For developer's quickstart page, use this:
```
---
layout: quickstart
title: "Developer's QuickStart"
type: test
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:
  - id: 1
    type: success
    description: If this is a recommended protocol, you can put explaination here. If none, remove this id 1 section.
    link: "if there is a reference link, you can link it here"
  - id: 2
    type: warning
    description: If this must used with caution, put explaination for the warning here. If none, remove this id 2 section.
    link: "if there is a reference link, you can link it here"
  - id: 3
    type: danger
    description: If this is no longer a good practive, put danger warning here. If none, remove this id 3 section.
    link: "if there is a reference link, you can link it here"
further-reading:
  - name: If there are more readings related to this topic, you can put the article name here.
    link: "Here is the placeholder for the link"
  - name: sample
    link: ""
  - name: sample
    link: ""
related-articles:
  - name: sample
    link: ""
  - name: sample
    link: ""
  - name: sample
    link: ""

---
Contents go here!
```

For IT's quickstart page, use this:
```
---
layout: quickstart
title: "IT's QuickStart"
type: test
image: /img/common/NewDevLogo.png
note: "Are you an IT administrator? Get started with best practice setup details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:
  - id: 1
    type: success
    description: If this is a recommended protocol, you can put explaination here. If none, remove this id 1 section.
    link: "if there is a reference link, you can link it here"
  - id: 2
    type: warning
    description: If this must used with caution, put explaination for the warning here. If none, remove this id 2 section.
    link: "if there is a reference link, you can link it here"
  - id: 3
    type: danger
    description: If this is no longer a good practive, put danger warning here. If none, remove this id 3 section.
    link: "if there is a reference link, you can link it here"
further-reading:
  - name: sample
    link: ""
  - name: sample
    link: ""
  - name: sample
    link: ""
related-articles:
  - name: sample
    link: ""
  - name: sample
    link: ""
  - name: sample
    link: ""

---
Contents go here!
```

For manager's quickstart page, use this:
```
---
layout: quickstart
title: "Manager's QuickStart"
type: test
image: img/common/NewDevLogo.png
note: "Are you a Manager? Get started with best practice setup details above."
col: col-md-8 col-sm-8 col-xs-8 infoBlocks
alerts:
  - id: 1
    type: recommend
    description: If this is a recommended protocol, you can put explaination here. If none, remove this id 1 section.
    link: "if there is a reference link, you can link it here"
  - id: 2
    type: warning
    description: If this must used with caution, put explaination for the warning here. If none, remove this id 2 section.
    link: "if there is a reference link, you can link it here"
  - id: 3
    type: danger
    description: If this is no longer a good practive, put danger warning here. If none, remove this id 3 section.
    link: "if there is a reference link, you can link it here"
further-reading:
  - name: sample
    link: ""
  - name: sample
    link: ""
  - name: sample
    link: ""
related-articles:
  - name: sample
    link: ""
  - name: sample
    link: ""
  - name: sample
    link: ""

---
Contents go here!
```

For page that is under construction, add the following under the content section:
```
Hi there! This page is currently under construction. If you would like to share your expertise relating to this topic with us , please <a href="CONTRIBUTING-template.md">click here!</a>

<img src="/img/common/under_construction.jpg" style="width:70%;height:70%;" alt="under construction image">
```


# Review & Deploy Process
### Review
Once a Pull Request has been opened, the team reviewing the changes may have questions or comments. Perhaps the coding style doesn't match project guidelines, the change is missing unit tests, or maybe everything looks great and props are in order. Pull Requests are designed to encourage and capture this type of conversation.

Everyone can continue pushing to their branch in light of discussion and feedback about their commits. If someone comments that you forgot to do something or if there is a bug in the code, you can fix it in your branch and push up the change. GitHub will show your new commits and any additional feedback you may receive in the unified Pull Request view.

The admin team looks at Pull Requests on a regular basis in a weekly triage meeting that we hold in a public Google Hangout. The hangout is announced in the weekly status updates that are sent to the puppet-dev list. Notes are posted to the Puppet Community community-triage repo and include a link to a YouTube recording of the hangout.

After feedback has been given we expect responses within two weeks. After two weeks we may close the pull request if it isn't showing any activity.

### Deployment
Once your pull request has been reviewed and the branch passes your tests, you can deploy your changes to verify them in the deveopment branch. If any branch causes issues, we can roll it back by deploying the existing master into production.

### Merging
Once the changes have been verified in production, it is time to merge your contents into the master branch! How exciting!
Once merged, Pull Requests preserve a record of the historical changes to your code. Because they're searchable, they let anyone go back in time to understand why and how a decision was made.

### Misc
GitHub Resource on Pull Request:
> Working on your first Pull Request? You can learn how from this *free* series, [How to Contribute to an Open Source Project on GitHub](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github).

GitHub Resource on GitHub Flow:
> Want to refresh on your understanding of the GitHub flow? You can find out more from the official guidance on [Understanding the GitHub Flow](https://guides.github.com/introduction/flow/).


# Ground Rules
### Expectated Behavior From All Of US

> Responsibilities
> * Ensure cross-platform compatibility for every change that's accepted. Windows, Mac, Debian & Ubuntu Linux.
> * Ensure that code that goes into core meets all requirements in the corresponding templates.
> * Create issues for any major changes and enhancements that you wish to make. Discuss things transparently and get community feedback.
> * Be welcoming to newcomers and encourage diverse new contributors from all backgrounds. See the [Python Community Code of Conduct](https://www.python.org/psf/codeofconduct/).
