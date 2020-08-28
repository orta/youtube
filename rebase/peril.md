### intro

I'm Orta Therox, a developer/designer working on the TypeScript team.
 
In the Apple developer ecosystem, there's a term called "Sherlocking" - it's used when a platform vendor (like Apple) re-implements an idea which previously was an indie app. 

The titular example came from when Apple took all of the ideas from an indie app by Karelia software called "Watson" into an upgrade of their app "Sherlock". It's wild, Apple gave Watson an award for best innovation in 2002, then in 2003 an update to Sherlock made it basically a carbon copy. In those situations, you really don't have much choice in the matter.

I've been sherlocked twice in my OSS career two big open source projects, on projects I've devoted years to, this is the story of the second one. Which starts right after the first.

This is a Rebase on How GitHub sherlocked Peril.

---- title card ----

About 5 years ago, I started wrapping up actively contributing to CocoaPods, a dependency manager for iOS and Mac projects. Think npm, or pip.
I stopped because Apple had announced their own equivalent to CocoaPods, Swift Package Manager, and it was only a matter of time before it became the main way people handled that problem given that they owned the platform.

This freed me up to tackled a problem I'd seen in maintaining a lot of large open source projects. Setting cultural norms.

Now bear with me, but I guess on an average day I handle or create about 10-20 pull requests across all the different orgs and repos I work with. If I make those pull requests, then I know the culture of the repo - for example does it use a CHANGELOG, does it use a specific format for commits, are labels important, are there README or documentation changes which need to happen when some code is changed.

If the PR comes from someone who is new, and is maybe a drive-by contributor, then they don't have all that cultural context. You can add a really long contribution guide which tries to inform someone of all possible interactions, but I've found most people don't read it.

So, I build a system called Danger from some of the code inside CocoaPods. Danger lets you write rules based on the pull request changes.

[split with some code]

So for example:

- you could detect if any code had changed in your app - then you can request that some tests were changed.
- you could ask for a CHANGELOG entry with every PR

Danger then provides that feedback inside a comment on the PR, and it means the maintainer does not need to ask for the same changes in every PR.

This is cool, and it meant for each repo you could set up a unique cultural norms and when the team agreed on a new norm, it could be built with code.

To skip a year or two, and an I started to ask myself - well, what if this was applied at organization level?

For example, can we write cultural rules like:

- All markdown files should have a spellcheck applied
- Any repo which has a CHANGELOG file, should request a changelog entry

This is what Peril is, it's cultural automation at the entire org layer. I used serverless functions to run the rules in sandboxed environments and they'd typically be done within a second.

At Artsy we explored a few cultural rules, and someone asked if we could build a "Merge on Green" feature into GitHub with it. 

Yeah, it turned out that building a generic system for handling cultural norms also turned out to be really good at automation at larger scale.

[split]

This system was based on you creating a repo, where you mapped GitHub webhooks to JavaScript or TypeScript files

```json
{
  "rules": {
    "create (ref_type == tag)": ["org/new_tag.ts", "org/updateDangerSystems.ts"],
    "pull_request.closed": "org/aeryn.ts",
    "pull_request": "org/changelog.ts",
    "issue_comment": "org/markAsMergeOnGreen.ts",
    "issues.opened": "org/checkTemplate.ts",
    "status.success": "org/mergeOnGreen.ts"
  }
}
```

For example, when an issue was opened, Peril would run `org/checkTemplate.ts` with the webhook JSON.

```ts
import { danger, markdown } from "danger"
import { Issues } from "github-webhook-event-types"

// Support checking if the issue has the same content as the issue template.
export default async (issueWebhook: Issues) => {
  const issue = issueWebhook.issue
  const repo = issueWebhook.repository

  // Grab, the issue template, it returns an empty string if a 404, so we can
  // do a check for existence
  const template = await danger.github.utils.fileContents(".github/ISSUE_TEMPLATE.md", repo.full_name)

  // Whitespace between code on disk vs text which comes from GitHub is different.
  // This took far too long to figure.
  if (template && template.replace(/\s+/g, "") === issue.body.replace(/\s+/g, "")) {
    markdown(
      `Hi there, thanks for the issue, but it seem that this issue is just the default template. Please create a new issue with the template filled out.`
    )

    // Let's just close it.
    await danger.github.api.issues.update({
      ...danger.github.thisPR,
      number: issue.number,
      state: "closed",
    })
  } else {
    console.log("The message did not match the template.")
  }
}
```

This meant that for any repo in the organization, if someone created a new issue which just contained the issue template then the issue would automatically be closed.

That is Peril in a nutshell. One of the cool parts of this technique was the JavaScript files lived in a separate repo, meaning I didn't have to worry about security issues like a Pull Request changing the JavaScript to leak secrets. Score.

We used Peril in Artsy for a while, and people started self-hosting their own versions. I got a few requests for having a centralized Peril server which anyone could sign up for, and so I started exploring hosting Peril myself as a service. 

Peril as a Service would be like having access to a very fast and testable  

I even had early-stage VCs, who you've probably heard of, reach out on the chance that I wanted to take funding for Peril as a company. I started building out peril as a service, and as I started to get close - I got an email about a meeting with some GitHub engineers who had been working on a new, big, project and they wanted me to test the alpha.

This turned out to be GitHub Actions, and it's not fair on the GitHub team to say they copied Peril which had been used in a few large JS teams at this point - we both were looking at the same problem domain and felt that a JS automation system based on the GitHub webhook system is an massive un-explored surface. It still is.

During the GitHub Actions alpha, I adding support for running Danger and ported a chunk of Peril's automation ideas into Danger so that it could run anywhere. However, until recently GitHub Actions had always limitations around secret tokens when running on open source repos. So, I still got a lot of use with Peril. 

When I was considering leaving my last job, one of the core ideas was that I could take peril and make it a 'lifestyle business' - something which pays the bills but doesn't consume my life, and gives me space to work on interesting OSS. I opted against that, too risky now there's a 500 pound microsoft gorilla in the room. On the flip side, that gave me the chance to take a risk on joining the TypeScript team, and I'm happy for that.

Today, there are still a few teams using Peril - it's a solid tool, and it's not going anywhere, I still accept PRs to it, got one last month, and have provided pretty reasonable migration paths inside Danger and using GitHub Actions.

Do you automate your GitHub PR workflow? ping me your favourite tool in the comments, and like if you enjoy JavaScript and subscribe regardless - tchaus!
