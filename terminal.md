New Terminal Setup
==================

[git + hub = github][hub]
-------------------------

hub is a command line tool that wraps `git` in order to extend it with extra
features and commands that make working with GitHub easier.

#### Installation with Homebrew

`hub` 2.x can be installed through Homebrew. Since it's in preview, you need to compile
from HEAD:

~~~ sh
$ brew install --HEAD hub
~~~

Aliasing
--------

Using hub feels best when it's aliased as `git`. This is not dangerous; your
_normal git commands will all work_. hub merely adds some sugar.

`hub alias` displays instructions for the current shell. With the `-s` flag, it
outputs a script suitable for `eval`.

You should place this command in your `.bash_profile` or other startup script:

~~~ sh
eval "$(hub alias -s)"
~~~

### Shell tab-completion

hub repository contains tab-completion scripts for bash and zsh. These scripts
complement existing completion scripts that ship with git.

* [hub bash completion](https://github.com/github/hub/blob/master/etc/hub.bash_completion.sh)
* [hub zsh completion](https://github.com/github/hub/blob/master/etc/hub.zsh_completion)


Commands
--------

Assuming you've aliased hub as `git`, the following commands now have
superpowers:

### git clone

    $ git clone schacon/ticgit
    > git clone git://github.com/schacon/ticgit.git

    $ git clone -p schacon/ticgit
    > git clone git@github.com:schacon/ticgit.git

    $ git clone resque
    > git clone git@github.com/YOUR_USER/resque.git

### git remote add

    $ git remote add rtomayko
    > git remote add rtomayko git://github.com/rtomayko/CURRENT_REPO.git

    $ git remote add -p rtomayko
    > git remote add rtomayko git@github.com:rtomayko/CURRENT_REPO.git

    $ git remote add origin
    > git remote add origin git://github.com/YOUR_USER/CURRENT_REPO.git

### git fetch

    $ git fetch mislav
    > git remote add mislav git://github.com/mislav/REPO.git
    > git fetch mislav

    $ git fetch mislav,xoebus
    > git remote add mislav ...
    > git remote add xoebus ...
    > git fetch --multiple mislav xoebus

### git cherry-pick

    $ git cherry-pick http://github.com/mislav/REPO/commit/SHA
    > git remote add -f mislav git://github.com/mislav/REPO.git
    > git cherry-pick SHA

    $ git cherry-pick mislav@SHA
    > git remote add -f mislav git://github.com/mislav/CURRENT_REPO.git
    > git cherry-pick SHA

    $ git cherry-pick mislav@SHA
    > git fetch mislav
    > git cherry-pick SHA

### git am, git apply

    $ git am https://github.com/defunkt/hub/pull/55
    [ downloads patch via API ]
    > git am /tmp/55.patch

    $ git am --ignore-whitespace https://github.com/davidbalbert/hub/commit/fdb9921
    [ downloads patch via API ]
    > git am --ignore-whitespace /tmp/fdb9921.patch

    $ git apply https://gist.github.com/8da7fb575debd88c54cf
    [ downloads patch via API ]
    > git apply /tmp/gist-8da7fb575debd88c54cf.txt

### git fork

    $ git fork
    [ repo forked on GitHub ]
    > git remote add -f YOUR_USER git@github.com:YOUR_USER/CURRENT_REPO.git

### git pull-request

    # while on a topic branch called "feature":
    $ git pull-request
    [ opens text editor to edit title & body for the request ]
    [ opened pull request on GitHub for "YOUR_USER:feature" ]

    # explicit title, pull base & head:
    $ git pull-request -m "Implemented feature X" -b defunkt:master -h mislav:feature

### git checkout

    $ git checkout https://github.com/defunkt/hub/pull/73
    > git remote add -f -t feature mislav git://github.com/mislav/hub.git
    > git checkout --track -B mislav-feature mislav/feature

    $ git checkout https://github.com/defunkt/hub/pull/73 custom-branch-name

### git merge

    $ git merge https://github.com/defunkt/hub/pull/73
    > git fetch git://github.com/mislav/hub.git +refs/heads/feature:refs/remotes/mislav/feature
    > git merge mislav/feature --no-ff -m 'Merge pull request #73 from mislav/feature...'

### git create

    $ git create
    [ repo created on GitHub ]
    > git remote add origin git@github.com:YOUR_USER/CURRENT_REPO.git

    # with description:
    $ git create -d 'It shall be mine, all mine!'

    $ git create recipes
    [ repo created on GitHub ]
    > git remote add origin git@github.com:YOUR_USER/recipes.git

    $ git create sinatra/recipes
    [ repo created in GitHub organization ]
    > git remote add origin git@github.com:sinatra/recipes.git

### git init

    $ git init -g
    > git init
    > git remote add origin git@github.com:YOUR_USER/REPO.git

### git push

    $ git push origin,staging,qa bert_timeout
    > git push origin bert_timeout
    > git push staging bert_timeout
    > git push qa bert_timeout

### git browse

    $ git browse
    > open https://github.com/YOUR_USER/CURRENT_REPO

    $ git browse -- commit/SHA
    > open https://github.com/YOUR_USER/CURRENT_REPO/commit/SHA

    $ git browse -- issues
    > open https://github.com/YOUR_USER/CURRENT_REPO/issues

    $ git browse schacon/ticgit
    > open https://github.com/schacon/ticgit

    $ git browse schacon/ticgit commit/SHA
    > open https://github.com/schacon/ticgit/commit/SHA

    $ git browse resque
    > open https://github.com/YOUR_USER/resque

    $ git browse resque network
    > open https://github.com/YOUR_USER/resque/network

### git compare

    $ git compare refactor
    > open https://github.com/CURRENT_REPO/compare/refactor

    $ git compare 1.0..1.1
    > open https://github.com/CURRENT_REPO/compare/1.0...1.1

    $ git compare -u fix
    > (https://github.com/CURRENT_REPO/compare/fix)

    $ git compare other-user patch
    > open https://github.com/other-user/REPO/compare/patch

### git submodule

    $ git submodule add wycats/bundler vendor/bundler
    > git submodule add git://github.com/wycats/bundler.git vendor/bundler

    $ git submodule add -p wycats/bundler vendor/bundler
    > git submodule add git@github.com:wycats/bundler.git vendor/bundler

    $ git submodule add -b ryppl --name pip ryppl/pip vendor/pip
    > git submodule add -b ryppl --name pip git://github.com/ryppl/pip.git vendor/pip

### git ci-status

    $ git ci-status [commit]
    > (prints CI state of commit and exits with appropriate code)
    > One of: success (0), error (1), failure (1), pending (2), no status (3)


### git help

    $ git help
    > (improved git help)
    $ git help hub
    > (hub man page)


Configuration
-------------

### GitHub OAuth authentication

Hub will prompt for GitHub username & password the first time it needs to access
the API and exchange it for an OAuth token, which it saves in "~/.config/hub".

### HTTPS instead of git protocol

If you prefer using the HTTPS protocol for GitHub repositories instead of the git
protocol for read and ssh for write, you can set "hub.protocol" to "https".
"hub.protocol" only applies when the "OWNER/REPO" shorthand is used instead of a full git URL.

~~~ sh
# default behavior
$ git clone defunkt/repl
< git clone >

# opt into HTTPS:
$ git config --global hub.protocol https
$ git clone defunkt/repl
< https clone >
~~~


[zsh-syntax-highlighting][syntax]
-----------------------
**[Fish shell](http://www.fishshell.com) like syntax highlighting for [Zsh](http://www.zsh.org).**


### Install with oh-my-zsh

* Download the script or clone this repository in [oh-my-zsh](http://github.com/robbyrussell/oh-my-zsh) plugins directory:

        cd ~/.oh-my-zsh/custom/plugins
        git clone git://github.com/zsh-users/zsh-syntax-highlighting.git

* Activate the plugin in `~/.zshrc` (in **last** position):

        plugins=( [plugins...] zsh-syntax-highlighting)

* Source `~/.zshrc`  to take changes into account:

        source ~/.zshrc


### How to tweak

Syntax highlighting is done by pluggable highlighter scripts, see the [highlighters directory](highlighters)
for documentation and configuration settings.


[hub]: https://github.com/github/hub
[syntax]: https://github.com/zsh-users/zsh-syntax-highlighting