# move fast

cd
cd ~
cd -
cd -<tab>

# make history

## exemple:

    # echo one two three
    one two three
    # echo un deux trois
    un deux trois
    # x=!?one?:2
    x=two

## exemple de la ligne courante

    @ ( "this WEIRD filename.txt" )
         cp $it $it:l~

    cp "this WEIRD filename.txt" !#:1:l~

## construire interactivement une commande

je veux me déplacer dans le répertoire qui contient le binaire de
ma commande perl6. avec un peu d'habitude de zsh (et si l'option
autocd est activée), la réponse est

     =perl6(:A:h)

     $(!!) replace le copier-coller

    which perl6
    readlink -f $(!!)
    dirname $(!!)
    cd $(!!)
    cd $(dirname $(readlink -f $(which perl6 )))/..

    which perl6 |
        xargs readlink -f |
        xargs dirname

# best of ~/.zshrc

autoload -Uz compinit
compinit
stty -ixo{n,ff}

    bindkey -v
    bindkey -s "((" "()\ei"
    bindkey -s "{{" "{}\ei"
    bindkey -s "[[" "[]\ei"
    bindkey -s "''" "'\ei'"
    bindkey -s '""' '"\ei"'

setopt autocd autopushd
setopt inc_append_history
setopt share_history

() {
	local keystroke widget
	for keystroke widget {
		bindkey $keystroke $widget
		bindkey -M vicmd $keystroke $widget
} } '\ee' edit-command-line \
	'^e'  edit-command-line \
	'^h'  run-help \
	'^r'  history-incremental-search-backward
