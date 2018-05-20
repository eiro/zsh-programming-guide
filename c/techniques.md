# documentation and comments

comments explain how to, documentation explain.

you can't comment inside a long line unless you
use the :+ substitution

    print -l some \
        ${:+this inline comment} \
        lines

# true in the nutshell

worst case scenario

    gpu=1
    [[ $gpu = 1 ]] && echo "processing ..."

[[ $gpu = 1 ]] retourne vrai, ce que fait la commande true.

    gpu=true
    $gpu && echo "processing ..."

il est aussi possible de créer des fonctions.

    gpu-enabled\? () true
    gpu-enabled\? && echo "processing ..."

pro variables: *localisation*(TODO) possible
pro fonctions: plus lisible ?

    enable  () $1-enabled\?() true
    disable () $1-enabled\?() false
    enable gpu
    gpu-enabled\? && echo "processing ..."

use prompt expansion to set a boolean

    true
	print -Pv PS1_GITSTATUS_UPDATE '%(?.true.false)'

can be short for

    if {true} { PS1_GITSTATUS_UPDATE=false } \
    else      { PS1_GITSTATUS_UPDATE=true  }

# gestion des paramètres

## tooling

ancien art: getopts et zargs ... voir le manuel

cf. manuel

## PBP: dérouler les variables

    local "v=${1?message d'erreur}"
    local "v=${1-valeur par defaut}"

## parametres nommés

    greetings () {
        local to
        eval "${(Mqe%)@:#?*=*}"
        echo hello ${to-$USER}
    }
    greetings
    greetings ls to='luke s. %m `hostname`'

# use of cat

## la syntaxe générique des filtres

* traitement des argument des filtres
    * liste de fichiers a traiter avec '-' signifiant stdin
      (./-) pour le fichier '-' présent dans $pwd
    * stdin par defaut
    echo $USER | cat <(hostname) - <(hostname)
    prometheus
    mc
    prometheus

## UUOC: useless use of cat
## PUOC (perlish use of cat)

    <> = <ARGV> = "act as a filter"

    cat "$@" | while {read line} {
    }

### cat = id

http://okmij.org/ftp/Computation/monadic-shell.html

# ergonomie d'une commande

* votre commande et le projet devrait s'appeller terminal-multiplexer
  * c'est assez explicite pour
    * être recherché (whence -am terminal)
    * ne pas être en conflit avec d'autres commandes
      (top-multiple-user-experience)
* *vous* devriez avoir une fonction dans votre ~/.zshenv

    ts () terminal-multiplexer split -d

une commande devrait idéalement être une phrase

    ip # montre la structure de la phrase
    ip address show dev eth0 # la phrase dans un script
    ip a s dev eth0          # la phrase dans la vie 

les arguments devraient être de type

     ▷  tmux ne -s work
     ambiguous command: ne, could be: new-session, new-window, next-layout, next-window

      ▷  tmux ne<tab>
      new-session  new    -- create a new session
      new-window   neww   -- create a new window
      next-layout  nextl  -- move a window to the next layout
      next-window  next   -- move to the next window in a session
