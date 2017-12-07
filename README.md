
This document provides instructions for working with the [draft] AV1 Bitstream
&amp; Decoding Process Specification.

The specification document is built from plaintext section and subsection
[Markdown] files (more specifically, [kramdown] files) using the [Jekyll] static
site generator tool.


## Building Locally

Contributors will want to preview their edits locally before submitting patches
for review. Doing so requires a sane Ruby and rubygems environment. We use
[rbenv] and [bundler] to "groom" the project environment and avoid conflicts.

**Note** that all commands are to be run as an ordinary, unprivileged user.


### Ruby and rbenv

This project currently depends on Ruby v2.4.1. Because your distro may lack this
version -- or installing it may conflict with your system's installed version --
first **[install rbenv]**, then install Ruby v2.4.1 within it (again, in
userland).

~~~~~ bash
# list all available versions:
$ rbenv install -l
2.2.6
2.3.0-dev
2.3.0-preview1
2.3.0-preview2
2.3.0
2.4.1

# install a Ruby version:
$ rbenv install 2.4.1
~~~~~

Depending on your distro and environment, you may have trouble building a
particular Ruby version. The rbenv project site maintains a
[wiki page with troubleshooting help](https://github.com/rbenv/ruby-build/wiki).


### Bundler

Gem dependencies are managed by [bundler].

~~~~~ bash
$ gem install bundler

# Filesystem location where gems are installed
$ gem env home
# => ~/.rbenv/versions/<ruby-version>/lib/ruby/gems/...
~~~~~


### Clone the Repo

~~~~~ bash
git clone git@github.com:AOMediaCodec/av1-spec.git
cd av1-spec
~~~~~


### Set Local Ruby Version (rbenv)

In the directory of your local clone, do:

~~~~~ bash
rbenv local 2.4.1
~~~~~

Regardless of any other Rubies installed on your system, the project environment
will now use v2.4.1 and gems appropriate for it.


### Install Gem Dependencies with Bundler

In the directory of your local clone, run

~~~~~ bash
bundle install
~~~~~

Bundler will set dependencies and install needed gems as listed in
`Gemfile.lock`.

**Note** that you may need Ruby development headers installed on your system
for some gems to compile successfully.


### Build and Preview Locally with Jekyll

~~~~~ bash
bundle exec jekyll serve
~~~~~

This will build the document and launch a local webserver at
`http://127.0.0.1:4000/av1-spec/` (by default). Jekyll will also watch the
the filesystem for changes and rebuild the document as needed. Reload your
browser tab to view any changes you've made.


### Notes on NPM and Grunt

_These steps are not critically necessary for working on the document. Rather,
they apply cosmetic changes to the HTML output on a postproc basis._

The specification document requires a bit of arbitrary text manipulation that
can't be done with Jekyll alone. To automate these needs we turn to [GruntJS], a
Node-based task runner. The following assumes you have already installed
[NodeJS] and [npm], the Node package manager.

~~~~~ bash
## Update npm globally
npm update -g npm

## Install grunt globally
npm install -g grunt-cli

## Go the the project directory
cd av1-spec

## Install the project's Node dependencies
## (uses package.json and Gruntfile)
npm install
~~~~~

To transform the Jekyll-generated HTML file (`_site/index.html`), run `grunt` in
the project directory. This will apply the text transformations described in
Grunt's `replace` task (see `Gruntfile`) and will write the output to
`docs/index.html`.

Currently this method is used to "bold" the names of syntax elements within
syntax tables. For example, the tokenized string `@@syntax_element` will be
replaced with `<b>syntax_element</b>`. This reduces the clutter of HTML elements
within the source text files.


[draft]: https://aomediacodec.github.io/av1-spec/
[Markdown]: https://daringfireball.net/projects/markdown/
[kramdown]: https://kramdown.gettalong.org/
[Jekyll]: https://jekyllrb.com/
[rbenv]: https://github.com/rbenv/rbenv
[bundler]: http://bundler.io/
[install rbenv]: https://github.com/rbenv/rbenv#installation
[GruntJS]: https://gruntjs.com/
[NodeJS]: https://nodejs.org/
[npm]: https://www.npmjs.org/
