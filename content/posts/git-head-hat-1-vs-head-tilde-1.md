---
title: "Git HEAD with caret and tilde"
tags: ["git", "note"]
date: 2019-02-28T14:10:45+01:00
draft: false
---

`HEAD~` or `HEAD~1` refer to the parent of the commit.
`HEAD~2` refer to the parents of parent of the commit, aka. grandparent

`HEAD^` or `HEAD^1` refer to the first parent of the commit.
`HEAD^2` refers to the second parent of the commit.

Suppose that I have a git repository like this

{{< highlight bash >}}
>> git log --graph --oneline
* c6ca995 (HEAD -> master) three.txt in master branch
*   9997436 Merge branch 'two'
|\
| * 0dda652 (two) two.txt in a branch
* | 5c224e8 two.txt in master branch
|/
* c131cae Add one.txt
* b8a505f Add README.md
{{< /highlight >}}

For getting just the parent of a commit, caret and tilde `^, ~` returns the same result.

{{< highlight bash >}}
>> git rev-parse --short HEAD~1
9997436

>> git rev-parse --short HEAD^1
9997436
{{< /highlight >}}

However, when we are moving from 1 to 2. There are differences. This will not work because the commit that `HEAD` are pointing to only has 1 parent.

{{< highlight bash >}} 
>> git rev-parse --short HEAD~2
5c224e8

>> git rev-parse --short HEAD^2
fatal: Needed a single revision
{{< /highlight >}}

Now, let dig a bit deeper on the caret. `^1, ^2` are for getting the first and second parents.`HEAD~1` points to the merge commit. This merge commit has 2 parents, the first parent is the commit in the master branch, the second parent is the commit from the branch that you merge into a master branch. This is how the caret works:

{{< highlight bash >}}
>> git rev-parse --short HEAD~1^1
5c224e8 # first parent, commit "two.txt in master branch"

>> git rev-parse --short HEAD~1^2
0dda652 # second parent, two.txt in a branch
{{< /highlight >}}

For the tilde `~`, it can go to find the parent, grandparent, grand-grandparent.... Hence `HEAD~1` will be `9997436`, `HEAD~2` will be `5c224e8`, etc.

{{< highlight bash >}}
>> git log master --first-parent --oneline
c6ca995 (HEAD -> master) three.txt in master branch
9997436 Merge branch 'two'
5c224e8 two.txt in master branch
c131cae Add one.txt
b8a505f Add README.md
{{< /highlight >}}

