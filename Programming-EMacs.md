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
