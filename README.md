Brume
=====

Brume is a lightweight static website manager built on top of [Git][1].

Basically, it’s a post-receive hook that puts the content of your repo to a
chosen directory, plus it applies some Git metadata (commit hashes, author
names, etc) to your files and generates an Atom feed of the changes you’ve done.

## Setup

Here are the steps you need to perform to use Brume

    $ cd where/you/want/the/repo
    $ git init --bare
    $ cp path/to/brume/post-receive hooks && chmod +x hooks/post-receive
    $ mkdir www && git config brume.worktree www
    $ git config brume.domain example.com

You can set other options to control various aspects of brume, see the
`head -16` of the `post-receive` file.

Once this is done, simply push your files to the repo and Brume will place them
in the folder specified by the `brume.worktree` option. Simply point a VHost to
this folder and ta-da, here's your website!

## Meta

You can use a set of placeholders in your files which will automatically be
replaced by the relevant Git metadata. This meta is obtained by looking at
the last commit which affects the file.

At the moment, Brume is not smart enough to rebuild only modified files, though
this is planned to be added in a near future.

The placeholders must be surrounded by `__`s. Here they are:

* `HASH`: the full commit hash
* `SHORT_HASH`: the abbreviated commit hash
* `AUTHOR`: the commit author
* `COMMENT`: the body of the commit message
* `SUBJECT`: the first line of the commit message
* `DATE`: the time the commit was done, respecting `brume.dateFormat`

## Todo-list

* Nicer changelog file
* Add (pre|post)-build hooks
* Smart building

[1]: http://git-scm.com/

