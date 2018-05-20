# awk

## nommer les colones

    getent passwd | awk -F: -vlogin=1 -vshell=7 '
        $shell ~ /zsh/ { print $login "est cool"}
    '

# virer la premiere ligne

    awk ' NR > 1 { print }'
    ⇒ { read; awk '{print}' }
    ⇒ awk '
        BEGIN {getline}
        {print}
    '

# awkish zsh filters

     sep=:
     print ${${(ps.$sep.)val}[1]}

     IFS=: read $fields <<< $line
     IFS=: read user\[$~fields] <<< $line

seq 5 | () {
    local it
    @- { echo $it }
}


