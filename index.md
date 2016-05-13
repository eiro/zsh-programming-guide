Le présent document est une introduction au shell scripting pour les
utilisateurs de langages dynamiques (perl, python, js, ruby, ...). Y sont
traités

* [ksh](https://en.wikipedia.org/wiki/Korn_shell) et l'implémentation qui fait
  référence à mes yeux ([mksh](https://www.mirbsd.org/mksh.htm)).
  ksh est présent sur de nombreux unices et est un tres bon choix quand chaque 
  Kbyte compte. 

* [standard POSIX actuel](http://pubs.opengroup.org/onlinepubs/9699919799/idx/shell.html)

* [zsh](http://zsh.org/) dont les fonctionnalités sont parfois plus à comparer
  avec les langages dynamiques qu'avec les autres shells. 

Un mot sur bash: son avantage est d'être le shell standard du GNU. Il est fourni
par défaut dans la plupart des distributions linux et je ne peux donc l'ignorer.
Il y est considéré dans le présent document comme une implementation bloated de ksh.

# hello world

* cycle de vie de la commande
    * REPL
    * eval = expansion + execution
    * expansion = variable, command, filename (globing)
* l'escaping et le quoting

# REPL and redirections

* byte oriented operator
* line oriented tools (mostly)
* read/write are blocking (-> meeting points, -> on demand)
* redirections
* how/why(not?) xml/json/... streaming data
  (functionnal programming langages, perl, powershell ... )

# variables

## scalars

* scalaires = strings : ubiquité comme en perl (c'est l'opérateur qui
  donne un sens au contenu de la variable)

# process communication

## the beauty

* Mc Illroy kiss principles
* pike/k unix programming env. intro
* cat-v

## the beast

subshells, scope and export, redirections, pipes and variables

### subshells

### math


* (( )) and $[]
* expressions separated by ','
* most of the C operators/syntax
* lot of builtins

    acos, acosh, asin, asinh, atan, atanh, cbrt, ceil, cos, cosh, erf, erfc, exp,
    expm1, fabs, floor, gamma, j0, j1, lgamma, log, log10, log1p, logb, sin, sinh,
    sqrt, tan, tanh, ...

[mathfunc](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fmathfunc-Module)

* expandable

    # math function cube takes 1 argument
    functions -M cube 1

    # when cube is 
    cube2 () (( $1 * $1 * $1 )) 

    (( val+=12,
       val = val == 23 ? 45 : val + cube(x),
       alert = val > max )) && print "oops"

## filename expansion

# notes on uze experiment

## goals and and tools

* js popularity became real with npm ecosystem (share code, docs and
  a deploy mecanism)
* js good parts is about working around the flaws
* let's try it with zsh with perl as inspiration

## possible workarounds

* fake builtins with aliases
* fake namespaces with dirpaths. failed because
    * tried symbol exporting using aliases which is basically
      silent monkey patching: danger!
    * dirpaths are not real namespaces so scopes aren't bound with dirpaths.
      * :: experiment failed because aliases are fragile (see ::)

# GARBAGE (le présent texte est de la prise de note. lire aussi e/zsh)

# variables

# declaration

    read x # lecture
    x=     # affectation
    scalaires = integer, float ou chaine
    liste=(
        les barewords 'et IFS'
    )

* [les variables](variables.html)
    * les associations

        que l'on parle de hash, map, tableau associatif, dictionnaire,
        association,

        nous parlons d'une liste de paires

        typeset -A  => my%

        my% user=(
            login     mc
            firstname marc
            lastname  chantreux )

        :bulb: perl hash slices

        login

        while {read} {
            IFS: read   \
            user[login] \
            user[x]     \
            user[uid]   \
            user[gid]   \
            user[gecos] \
            user[home]  \
            user[shell] <<< $REPLY
        }

        gecos_fields=( login x uid gid gecos home shell )

        my@ fields=( nom prenom )
        my% client
        IFS=: read client[nom] client[prenom] <<< "chantreux:marc"

        set -x
        fields=( nom prenom )
        my% client
        IFS=: read client\[nom] client\[prenom] <<< "chantreux:marc"
        IFS=: read client\[{nom,prenom}] <<< "chantreux:marc"
        IFS=: read client\[$^fields] <<< "chantreux:marc"
        print "$client[nom]"


        gecos_fields=( login x uid gid gecos home shell )
        my% mc
        l IFS=: read user\[$^gecos_fields]
        getent passwd mc | cat



        gecos_fields=( login x uid gid gecos home shell )

        the awk way


zsh pour les programmeurs
* notion de poweruser
* avant, tout le monde passait par le "bizutage" : shell + vi pour lancer son X
* le formalisme textuel
  * combiner des outils
  * automatiser
  * souplesse
  * décrivent certains problèmes plus simplement
* aujourd'hui, UI -> programmation

si pas programmeur:
    acces a des concepts puissants qui
    * deviennent le paradigme standard
    * permettent d'écrire des choses extremement puissantes de manière concise
    * le tout en manipulant peu de concepts

si programmeur:

functionnel impur:

    * passage de fonctions, applications partielles, générateurs
    * permettant la manipulation de structures complexes
    * parallèle (et même distribué)
    * extensible très simplement dans n'importe quel langage de programmation
    * disposant de la REPL la plus utilisée et la plus utile au monde

la façon dont il faut structurer sa pensée est bien cell

TODO Intro:

Nous verrons que les pipes permettent de combiner des générateurs
* générateurs, stateless, on demand

* pas de cloture syntaxique mais des générateurs
* pas d'objets ou de structures arborescentes mais des répertoires
* pas de namespaces mais des chemins
* pas de références mais des symboles

* tout garder global
* eviter l'enfer des quotes (ni trop ni pas assez)

format=(
    procs  'r v'
    memory 'swpd free buff cache'
    swap 'si so'
    io 'bi bo'
    system 'in cs'
    cpu 'us sy id wa st'
)


massoc-reader/2 () {
    local reader=$1 evaluer=$2
    shift 2
    my@ fields
    for k vs ($argv) {
        my% $k
        fields+=( $k'\['${(s: :)^vs}] )
    }
} 

$format
vmstat|seq -n 3p| eval $reader
print $memory[swpd]


# # vmstat 
# procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
#  r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
#  0  0   1132 134084 247800 550568    0    0     7     7   52   79  2  1 98  0  0
