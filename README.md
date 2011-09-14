Brume
=====

Brume is a lightweight static website manager built on top of [Git][1].

Basically, it's a post-receive hook that pulls out changes you've made to a
given directory, running a script on the files and generating an Atom feed of
updates.

You can use your own builder script, the default one being `/bin/cp`.
You can also use a custom post-processor of your choice.

## Requirements and basic setup

Brume is written in Bash (tested with GNU bash 4.2) and requires only standard
tools (grep, sed,…)

Here are the steps you need to perform to use Brume

    $ cd where/you/want/the/repo
    $ git init --bare
    $ cp path/to/brume/post-receive hooks && chmod +x hooks/post-receive
    $ mkdir www && git config brume.output $(pwd)/www
    $ git config brume.feed.domain <website url>

You can set other options to control various aspects of brume, see the
`head -25` of the `post-receive` file.

Once this is done, simply push your files to the repo and Brume will place them
in the folder specified by the `brume.output` option. Simply point a VHost to
this folder and ta-da, here's your website!

## Settings

* `brume.output`:
  Defines the directory where brume will put the contents of the repository
* `brume.builder`: Foo bar!

## Todo-list

* Add a setup script

[1]: http://git-scm.com/

