# Module 0408: What's up with GitHub and Open Educational Resources?

[GitHub](https://github.com) is a web-based repository for all kind of projects. One of the original purposes of `GitHub` is for coding. However, it is also well suited to any content that is text-based. If OER (open educational resources) is created in a text-based format, `GitHub` is, potentially, a great place to host the content.

# Getting Started

1.  Go to [GitHub](https://github.com) and sign up for an account or sign in if you already have an account.
2.  Click "New"

That's it! Well, not really. Let us go over the concepts involved.

The term "repository" refers to a resource where:

* It can host a variety of files and folders. In a sense, a repository is similar to a file system.
* The content stored in a repository is revision-controlled.

What does "revision-controlled" mean? It means a lot of things, including the following:

* Changes are tracked. A file can be reverted to an earlier version.
* The current state of a file can be compared to earlier version to see the differences.
* A repository can be "cloned." This means another party, if permitted, can duplicate all the files of a repository.
* Multiple parties can simultaneously make changes to even the same files as long as the changes are not conflicting.
* A version can be "forked." This creates multiple versions of the repository so that the changes made to each branch stays independent from each other.
* Branches of a repository can be "merged", meaning that the changes converge to a single branch.

## Granularity of a repository

There is hard-and-fast rules. If the granularity is too fine, then the author ends up with many repositories. This can make projects difficult to maintain. On the other hand, if the granularity is too coarse, then it is difficult to another person to make only one change to s small part of the project. 

At the end of the day, text files are relatively small. If the OER is in book form, then it makes sense that each book has a repository. However, if the OER is in smaller independent modules, then a single repository to host all the modules makes sense.

## Naming of a repository

In order for others to quickly locate content, it is best not to make the name of a repository too complex. The URL to a single file of a repository contains the author's account name as well as the name of the repository. Therefore, there is no need to duplicate these components in the name of a file in a repository.
