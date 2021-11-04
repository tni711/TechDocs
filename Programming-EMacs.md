## Install Emacs 27
sudo add-apt-repository ppa:kelleyk/emacs
sudo apt update
sudo apt install emacs27

## Silversearcher
apt-get install silversearcher-ag

## ripgrep
sudo add-apt-repository ppa:x4121/ripgrep
sudo apt-get update
sudo apt install ripgrep

## snap install
sudo snap install ripgrep --classic

## Helm completion
checkout URL below for the concept and setup details
https://tuhdo.github.io/helm-intro.html
https://emacs-helm.github.io/helm/#introduction
https://writequit.org/denver-emacs/presentations/2016-03-01-helm.html


## Auto Format
Lets you auto-format source code in many languages using the same
command for all languages, instead of learning a different elisp
package and formatting command for each language.

Just do M-x format-all-buffer and it will try its best to do the
right thing.

URL https://github.com/lassik/emacs-format-all-the-code
install melpa package --> format-all


## rtags / rdm / rc
https://vxlabs.com/2016/04/11/step-by-step-guide-to-c-navigation-and-completion-with-emacs-and-the-clang-based-rtags/


## C++ / ycmd
https://github.com/abingham/emacs-ycmd
need to generate compilation json file before ycmd auto complete will works
goto source directory and do
> cmake -DCMAKE_COMPILE_COMMANDS=1 .


## Profile Setup
See URL below for good tutorial of EMACS
URL of Mike Zamansky's Emacs Tutorial of how to setup this up
http://cestlaz.github.io/stories/emacs/

Keybindings
https://caiorss.github.io/Emacs-Elisp-Programming/Keybindings.html


## Guide to irony-server for autocomplete
http://tuhdo.github.io/c-ide.html


## Which key
Brings up some help
URL https://github.com/justbur/emacs-which-key


## Avy Char Search
See https://github.com/abo-abo/avy for more info

## Silversearcher
apt-get install silversearcher-ag

## Ivy / Counsel / avy
Swiper gives us a really efficient incremental search with regular expressions
and Ivy / Counsel replace a lot of ido or helms completion functionality
URL https://sam217pa.github.io/2016/09/13/from-helm-to-ivy/

### IBUFFER
;; In an Emacs session, you may have a lot of buffers, including non-file buffers such as shell buffers, email buffers¡­
;; How do you manage buffers when it's getting large? C-x C-b executes list-buffers, provide you a list of buffer in which
;; you can search. However, list-buffers is a simple command for buffer management.
;; Emacs also provides ibuffer, which is a superior alternative

### C++ / Rtags
[rtags install]https://github.com/Andersbakken/rtags
[rtags usage]https://github.com/Andersbakken/rtags/wiki/Usage

;; Global with exuberant-ctags and pygments plugins can support dozens of programming languages.
;; see URL for detail GNU Global documentation
;; https://www.gnu.org/software/global/


### Atomic Chrome (edit in emacs)

```
	#+BEGIN_SRC emacs-lisp
	(use-package atomic-chrome
	:ensure t
	:config (atomic-chrome-start-server))
	(setq atomic-chrome-buffer-open-style 'frame)
	#+END_SRC

	### PDF tools
	#+BEGIN_SRC emacs-lisp
	(use-package pdf-tools
	:ensure t)
	(use-package org-pdfview
	:ensure t)

	(require 'pdf-tools)
	(require 'org-pdfview)
	#+END_SRC
```


### Google Chrome
Install google-chrome-stable
URL : https://www.google.com/chrome

```
	#+BEGIN_SRC emacs-lisp
	(setq browse-url-browser-function 'browse-url-generic
		browse-url-generic-program "google-chrome-stable")

	(setq auto-window-vscroll nil)

	#+END_SRC
```

### rtags build
    https://github.com/Andersbakken/rtags#optional-1
    make sure set PATH to lua5.3/bin after compilation

# Sqlite3 Tool
  https://github.com/sqlitebrowser/sqlitebrowser


# Install clang/LLVM
https://llvm.org/


## Install clang/llvm
Installing llvm 3.9 can easily be done under Xenial Xerus by using the 'LLVM Debian/Ubuntu nightly packages' PPA. Just follow the steps below:

    Add the archive signature:

    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -

    Add the PPA:

    sudo apt-add-repository "deb https://apt.llvm.org/xenial/ llvm-toolchain-xenial-3.9 main"
    sudo apt-get update

    Note: There may be some authentication warnings for the llvm key which I have safely overridden on my own system. To bypass authentication, replace sudo apt-get update with

    sudo apt -o Acquire::AllowInsecureRepositories=true update

    Allow the Repository to reload and then run the following command:

    sudo apt-get install clang-3.9 lldb-3.9

    Test your installation as follows, as shown on my own Xenial system:

    $ clang-3.9 --version
    clang version 3.9.0-svn275716-1~exp1 (trunk)
    Target: x86_64-pc-linux-gnu
    Thread model: posix
    InstalledDir: /usr/bin

## Making latest version available as clang
https://blog.kowalczyk.info/article/k/how-to-install-latest-clang-6.0-on-ubuntu-16.04-xenial-wsl.html

This version is installed side-by-side with the default clang 3.8. To run it, you have to explicitly say clang-6.0. clang will either refer to 3.8 (if you¡¯ve installed it) or nothing at all.

You can reconfigure the system so that clang refers to clang 6:

>sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.8 100
>sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-5.0 800
>sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 1000
>sudo update-alternatives --install /usr/bin/clang++ clang /usr/bin/clang-3.8 100
>sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.8 100
>sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-5.0 800
>sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 1000
>sudo update-alternatives --config clang
>sudo update-alternatives --config clang++


http://llvm.org/

## Build from source
list tags info
svn ls -v http://llvm.org/svn/llvm-project/llvm/tags
check out a particular tag version

Build from source
http://clang.llvm.org/get_started.html

mkdir $HOME/llvm-6.0.1
cd $HOME/llvm-6.0.1
svn co http://llvm.org/svn/llvm-project/llvm/tags/RELEASE_601/final $HOME/llvm
cd $HOME/llvm-6.0.1/llvm/tools
svn co http://llvm.org/svn/llvm-project/cfe/tags/RELEASE_601/final clang
cd $HOME/llvm-6.0.1/llvm/tools/clang/tools
svn co http://llvm.org/svn/llvm-project/clang-tools-extra/tags/RELEASE_601/final extra
cd $HOME/llvm-6.0.1
mkdir build
cmake -G "Unix Makefiles" ../llvm
make


# rtags
https://github.com/Andersbakken/rtags
http://diobla.info/doc/rtags

RTags is a client/server application that indexes C/C++ code and keeps
a persistent file-based database of references, declarations,
definitions, symbolnames etc. There¡¯s also limited support for
ObjC/ObjC++. It allows you to find symbols by name (including nested
class and namespace scope). Most importantly we give you proper
follow-symbol and find-references support. We also have neat little
things like rename-symbol, integration with clang¡¯s ¡°fixits¡±
(http://clang.llvm.org/diagnostics.html). We also integrate with
flymake using clang¡¯s vastly superior errors and warnings. Since RTags
constantly will reindex ¡°dirty¡± files you get live updates of compiler
errors and warnings. Since we already know how to compile your sources
we have a way to quickly bring up the preprocessed output of the
current source file in a buffer.

While existing taggers like gnu global, cscope, etags, ctags etc do a
decent job for C they often fall a little bit short for C++. With its
incredible lexical complexity, parsing C++ is an incredibly hard task
and we make no bones about the fact that the only reason we are able
to improve on the current tools is because of clang
(http://clang.llvm.org/). RTags is named RTags in recognition of
Roberto Raggi on whose C++ parser we intended to base this project but
he assured us clang was the way to go. The name stuck though.

rtags is made of 2 programs:
    rdm, a server that index files and handles database queries.
    rc, the client to control rdm (make queries, set project configuration, ¡­)

## build from source
git clone --recursive https://github.com/Andersbakken/rtags.git
cd rtags
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=1 .
make


# rtags
https://github.com/Andersbakken/rtags
http://diobla.info/doc/rtags

RTags is a client/server application that indexes C/C++ code and keeps
a persistent file-based database of references, declarations,
definitions, symbolnames etc. There¡¯s also limited support for
ObjC/ObjC++. It allows you to find symbols by name (including nested
class and namespace scope). Most importantly we give you proper
follow-symbol and find-references support. We also have neat little
things like rename-symbol, integration with clang¡¯s ¡°fixits¡±
(http://clang.llvm.org/diagnostics.html). We also integrate with
flymake using clang¡¯s vastly superior errors and warnings. Since RTags
constantly will reindex ¡°dirty¡± files you get live updates of compiler
errors and warnings. Since we already know how to compile your sources
we have a way to quickly bring up the preprocessed output of the
current source file in a buffer.

While existing taggers like gnu global, cscope, etags, ctags etc do a
decent job for C they often fall a little bit short for C++. With its
incredible lexical complexity, parsing C++ is an incredibly hard task
and we make no bones about the fact that the only reason we are able
to improve on the current tools is because of clang
(http://clang.llvm.org/). RTags is named RTags in recognition of
Roberto Raggi on whose C++ parser we intended to base this project but
he assured us clang was the way to go. The name stuck though.

rtags is made of 2 programs:
    rdm, a server that index files and handles database queries.
    rc, the client to control rdm (make queries, set project configuration, ¡­)

## build from source
git clone --recursive https://github.com/Andersbakken/rtags.git
cd rtags
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=1 .
make
