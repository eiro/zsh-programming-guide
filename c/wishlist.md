# array subscripts

this works

    a=()
    read a\[{1,4}] <<< "in out"
    echo "1: $a[1]"
    echo "4: $a[4]"
    echo "3: $a[3]"
    echo "#: $#a"

so should

    echo $a[{1,4}]

but it don't

# namespaces

this is actually possible

    this/awesome/utils/namespace/level/show () {
        echo we are now at level $1
    }

    this/awesome/utils/namespace/start () {
        local level=${1:-}
        this/awesome/utils/namespace/level/show $level
    }

this should be possible

    this/awesome/utils/namespace/start () {
        local -n level=${1:-}
        .../level/show $level
    }

* local -n to be available only in the namespace
* ... to refer to the current namespace

# level up the world with zsh awesomeness

zle and extendedglob should be

* external libraries bindable by anything else than zsh
* still scriptable in zsh

zsh could be an extension langage (the way lua and guile are)

# completion server

for the ones of us who are frequently scripting, it could be nice to use
a zsh process to provide completion. the vim part isn't the problem but i
don't know how to connect to zsh.

# filename expansion modifiers should be available in array manipulation

TODO: provide examples here
