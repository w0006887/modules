---
title: "Module 0422: Introduction to `git`"
---

# _{{ page.title }}_

# What is `git`?

`git` is a tool designed for collaboration in terms of coding. However, `git` can also be used for projects that involve mostly or wholly documentation. `git` works best for source material that is in plain text.

# Concepts

## Files, folders and objects

From the user's perspective, `git` works with files and folders. However, regular files and folders are represented as objects internally. Most users do not need to understand or access the underlying objects.

## Repository

A repository refers to the underlying objects representing the files and folders that are revision-controlled. A repository can be local, meaning that it exists in the same file system as the files and folders that are being represented. In this context "in the same file system" is almost the same as saying "on the same computer."

A remote repository consists of the objects that are used to represent files and folders, but such objects exist on a remote computer that is accessible via networking.

A remote repository can be `clone`d to a local repository so that a user can view and edit the files and folders. Note that a remote repository can be simultaneously `clone`d to multiple local repositories on different computers. As a result, files and folders can be modified by multiple users at the same time.

## Commit

A `commit` applies to a local repository. A `commit` updates the objects of a local repository to record the modifications of files and folders.

Because a `commit` is local, a user can perform as many commits as practical to keep track of changes. `git` offers tools to show differences between commits. This is helpful to find out changes between commits as a part of debugging.

## Push

A `push` first analyzes all the modifications of a local repository since the initial `clone` or the last `push`. Then these modifications are sent to and integrated into the associated remote repository.

A `push` should occur only after the user of the local repository has achieved a milestone of a roadmap that the team has agreed upon. This often means the code that is pushed should be debugged and has been verified to meet all the specifications as agreed.

Each `push` is an atomic event. If two local repositories are pushing at the same time, one will be completed before the other one starts.

Note that a `push` does not automatically propagate the modifications to all the local repositories that are associated with the remote repository.

## Pull

A `pull` queries the remote repository and analyzes all the modifications to the remote repository since the initial `clone` or the previous `pull` operation. Then the modifications are applied to the local repository where the `pull` operation is executed.

A `pull` allows the user of a local repository to bring in all the released (pushed) updates from other teammates.

## Branch

Every repository starts with a default `MAIN` branch. A single branch is a chain of `push` operations.

`branch` is also an action. A remote repository can be branched to create additional parallel chains of push operations.

