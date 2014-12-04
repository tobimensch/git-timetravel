# Install

Just download git-timetravel from this repository and put it somewhere in your PATH. You're done.

Unless you don't have python, then you need to get python first. And also the docopt module.

# Description

git-timetravel makes it easier for git users to checkout previous commits and to go back and forth between them. I.e. they can go back by one commit, then try to see if a regression occurs at that state, then they can go back by one more commit, try again, go back by one more commit, try again, and so on.
They can also go back a number of commits or even forward. When they're done they just type "git timetravel anchor" and git-timetravel takes them back to (the future) where they were before they started to explore older commits using git-timetravel. The local changes, if there were any, will be restored, so you'll not have to worry that any of your data will be lost.

When you're in one of the older commits, be aware that the HEAD is set to that commit and if you make changes and commit that this will create a new branch at this point, and when you return to the anchor, then this branch will be a side-branch to your real branch. Garbage collection will eventually eliminate this branch. But git-timetravel also stashes changes you make to earlier commits for you. So when you don't commit them you could just later try to merge those changes when you're back at the anchor.

The "home-point", "where you came from", the "recent commit" HEAD pointed to before you started to timetravel your git repository is called "anchor". The project takes suggestions for a better name. But in the meantime we call it anchor (point).

# How it's used

So you're in your git repository and somewhere in the last dozen of commits stuff broke, but you don't know where.
You start by going back 2 commits because you know that this issue existed at least in the last commit, too.

    git timetravel back 2

Now you're exactly 2 commits back. You'll see that in your git log the latest to commits aren't showing up and
your HEAD now points exactly to the current commit.
You can now test i.e. if a regression exists here. You notice it still does. You decide to go back one more commit.

    git timetravel back

You repeat your testing, still the bug exists. Now you're really going for it and you go back 20 commits.

    git timetravel back 20

Yeah, finally that nasty bug is gone. But where was it introduced? You go forward 10 commits.

    git timetravel forward 10

Oh, no, it's here again. At least you know the range now. You go back 5 commits.

    git timetravel back 5

Now the regression is gone, let's go forward one-by-one.

    git timetravel forward

The regression returns. And now you know that it happened in this commit. You can now view the differences between
this commit and the one before and you'll likely find where the bug is.
Now that you know where the bug is you can stash a bugfix or let git-timetravel let it do for you automatically.
Or you create a patch, or you just make a note in your head. Now is the time to return to the anchor.

    git timetravel anchor

Your timetraveling session is now over. With your new knowledge from the past you can now finally fix that nasty
regression.

# Bugs / Development / Testing / Feedback

The github issues page of git-timetravel is the right place for all of that:
https://github.com/tobimensch/git-timetravel/issues

