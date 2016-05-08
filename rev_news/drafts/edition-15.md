---
title: Git Rev News Edition 15 (May 11th, 2016)
layout: default
date: 2016-05-11 21:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 15 (May 11th, 2016)

Welcome to the 15th edition of [Git Rev News](http://git.github.io/rev_news/rev_news.html),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](http://git.github.io/rev_news/rev_news.html) on [git.github.io](http://git.github.io).

This edition covers what happened during the month of April 2016,
especially at the Git Contributor Summit on April 4 2016 and at the
Git Merge conference on April 5 2016.

## Discussions

### General

* Discussions at the Git Contributor Summit, part 2, about misc topics

At the Git Contributor Summit on April 4th, just after the lunch
break, the state of the participation of the Git project in the Google
Summer of Code (GSoC) and Outreachy was briefly mentioned, then Jeff
King, alias Peff, talked about the state of the Git project as part of
the [Software Freedom Conservancy (SFC)](https://sfconservancy.org/).

Git is one of the SFC Member Projects. The SFC manages the legal and
administrative aspects of the Git project. The SFC also manages Git's
money, which amounts to around $20000. This money comes mostly from
donations made on git-scm.org, GSoC mentor stipends and book
royalties. The money has been used in the past to pay for some
developers to travel to conferences like Git Merge. It may be used in
the future to pay Outreachy student stipends.

The governance of the Git project as part of the SFC is in the hands
of Junio Hamano, Shawn Pearce and Jeff King. The main activity of the
governance consists in handling trademark issues related to the "Git"
trademark that the project owns.

There are a number of projects who call themselves Git XXX and the
trademark policy on git-scm.org is used to decide if those trademarks
are approved or not.

Another activity is related to defending the license which is the
GPLv2. There have been some vendors who distributed Git with some
changes, but did not provide the source code of the Git version they
distributed. For now it has been possible to resolve these cases, but
it is not completely clear if some vendors currently fullfill all
their obligations. In case some developers who contributed to Git
wants to take a close look at what the vendors are doing, the SFC can
help them.

After that SubmitGit was discussed as well as ways to make it easier
for people who are not yet Git developers to contribute. TravisCI
which can be used to automatically test pull requests that are
submitted on GitHub was also discussed at the same time.

It appeared that it would be good to also be able to test pull
requests on Windows machines but TravisCI doesn't support Windows
yet. To help on this GitLab CEO, Sytse "Sid" Sijbrandij, offered to
let the project use GitLab CI which supports Linux, OSX and Windows.

Various subjects were then discussed a bit, like case insensitive
refnames and filenames, submodules and Git on Celph which is a file
system for computer clusters.

A mix of long time and quite new Git contributors, along with people
from Git related projects and companies attended. The atmosphere was
relaxed and informal. Overall it was a very pleasant event.

* [20 Tricks with Git and Shell](https://speakerdeck.com/nibalizer/20-tricks-with-git-and-bash)

At the [Git Merge conference](http://git-merge.com/) on April 5th 2016
at [New World Stages](http://newworldstages.com/) in New York City,
USA, Spencer Krum, who works for IBM in Portland and appears to be a
big fan of the
[SFC (Software Freedom Conservancy)](https://sfconservancy.org/), gave
an interesting and fast-paced presentation about some shell and Git
command line tricks.

Some of the tricks he showed are available in his
['bash-tricks' GitHub repository](https://github.com/nibalizer/bash-tricks).

The presentation started with simple shell aliases like `alias
sl='ls'` to cope with typos and `alias g='git'` to reduce typing, then
a bit more complex ones to avoid typing common arguments like `alias
gprom='git push origin master'` and `alias pydoc='python -m pydoc'`,
until validation aliases like:

```
alias yamlcheck='python -c "import sys, yaml as y; y.safe_load(open(sys.argv[1]))"'
```

Then Spencer spoke about customized prompts for git, filesystems and
tools, and about git config aliases, for example:

```
[alias]
	sgrep = "!f() { git submodule foreach \"git grep '$1'; true \"
			| grep -B 1 \"$1\"; }; f"
```

After that came functions. Some were general like:

```
# Get to the top of a git tree
cdp () {

  TEMP_PWD=`pwd`
  while ! [ -d .git ]; do
  cd ..
  done
  OLDPWD=$TEMP_PWD

}
```

Others were related to Gerrit or GitHub:

```
# Check out a Pull request from github
function pr() {
  id=$1
  if [ -z $id ]; then
      echo "Need Pull request number as argument"
      return 1
  fi
  git fetch origin pull/${id}/head:pr_${id}
  git checkout pr_${id}
}
```

In the end Spencer showed how to combine multiple small features to
get something interesting. First vim can be started at a given line by
giving the line in a +[num] argument, for example `vim +24`, then one
can get the previous command typed on the command line using
`history | tail -n 2 | head -1`, and finally one can use `git grep -n XXX`
to get a grep result from Git with a line number.

These 3 small tricks can be used in the following big one:

```
# Have vim inspect command history
vim () {
    last_command=$(history | tail -n 2 | head -n 1)
    if [[ $last_command =~ 'git grep' ]] && [[ "$*" =~ :[0-9]+:$ ]]; then
        line_number=$(echo $* | awk -F: '{print $(NF-1)}')
        /usr/bin/vim +${line_number} ${*%:${line_number}:}
    else
        /usr/bin/vim "$@"
    fi
}
```

That makes vim open file "foo" at line "X" if one uses `vim foo:X`
just after having run `git grep`.

* [GSoC 2016](http://thread.gmane.org/gmane.comp.version-control.git/292308/)

This year only one student, Pranit Bauva, will participate in the
Google Summer of Code 2016 under the Git project. He will work on
incrementaly rewriting in C the parts of "git bisect" that are still
in shell. He will be mentored by Lars Schneider and Christian Couder.

<!---
### Reviews
-->

<!---
### Support
-->

## Releases


## Other News

__Various__



__Light reading__


__Git tools and sites__


## Credits

This edition of Git Rev News was curated by Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Thomas Ferris Nicolaisen &lt;<tfnico@gmail.com>&gt; and Nicola Paolucci &lt;<npaolucci@atlassian.com>&gt;,
with help from XXX.