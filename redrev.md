# redrev

A "redecentralized revision control system".

Overarching vision: increase decentralization over `git` / dethrone `github`, censorship resistance for software development.

## Features

### Fantasy perfection on deployment engineering

Since this is a fantasy project, all that shit just works beautifully and everyone gets it. The core is simple, thin, and consistent. There's a good single library for each language of your choice. There's a single cli tool that's high enough level that there aren't a billion customized plugins, and yet simple enough that it's not bewildering. The UX is easy to pick up and remember and powerful.

### Simplistic node encryption

Encrypt node contents, but maybe fs/revision/metadata tree structure is visible (because that's harder to protect efficiently). Follow `tahoe-lafs` immutable node style with delegated read access, so a revision link includes the decryption key transitively.

**Why?** Seamlessly allow using the tool for either private or public data, without imposing any structure on how users organize their repos.

### Only Signers Create Revision

A revision is inexorably bound to a cryptographic signature verifier. A human user probably has one of these per checkout, and they are created willy nilly, for example if you initialize a new repo or clone an existing one, the tool just sticks one right there with the checkout. The signature verifier is *the fundamental "branch-like" reference*.

**Why?** Removes a baked-in repo/branch namespace (which leads to a centralized namespace keeper). Also ensures every revision is attested to cryptographically for auditability.

### Network Independence

The authentication and authorization of creating repositories, pushing to them, sharing them with others, etc… should be network independent for everything except data availability (and censorship resistance?). So there are no equivalent of `git remotes`: if you want to pull from a specific revision signer, you can get their updates through multiple network mechanisms. Likewise for pushing your own changes.

This one is harder to do well, especially when we take into account UX + availability + censorship resistance.

**Why?**

- Remove dependence on a namespace / availability gatekeeper for all repositories.
- Simpler UX for the happy cases. Example: Want to publish new revisions? You don't need an account, just push. Want to do another clone of a repo you've already fetched? Great, the local store already has it.

### In-Band Ticketing and Pull Requests

Issue tracking and pull request lifecycle are built into the base layer.

**Why?** Avoid centralized gatekeepers to organize software development. Automate these concerns at higher levels with standardized tools.

### In-Band Revision Constraints

A revision can introduce deterministic, final, pure predicates on all descendent revisions.

**Why?** Use this for QA / style enforcement, etc… "Peer-to-peer Revision Correctness Consensus"

### Explicit Refactoring w/ Garbage Collection

Want to do things like rebases, cherry picking, stashing? No problem, just proceed committing as normal and these operations are explicitly codified in the revision control information. Example: "This revision is a rebase of X onto Y." Front-end tools then present the "story" revisions typically, but if you need to muck around in the "refactoring" revisions you may. You may also release those to garbage collection if you're no longer interested.

**Why?**

- Explicit protocol support for these common operations allows better collaboration tools and UX.
- Avoid weird "commit-like" constructs which can just be standard revisions, ex: `git stash`, a lot of branch management, no more force pushes, etc…

### subtrees on acid

The base tool supports "subtrees" directly, transparently, and natively, where a path inside a repo is associated with one or more upstream revision signers. You know this goal is met when everyone just starts making `/` a repository and all other repos on the filesystem become subtrees.

**Why?** Make permissionless composition of repositories seamless and easy. Put everything in a mono repo if you want. Wrap public projects with your private project repo.

### org tech(?)

Should the tool be integrated into some kind of "org tech" like DAOs, aftok, etc? Not sure how much to merge these different layers.

**Why?** Overthrowing the gatekeepers for software development doesn't only require tools to get the job done, but it requires coordinating human action sustainably over large scales and time.
