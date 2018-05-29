just random notes for the moment



    l 1 50 70 100           |
        @- {l $it; sleep 1} |
        zenity --progress

        cool=()
        l those are it |

getlines () {
	local _
	IFS=$'\n' read -d '' "$@" _
}

cool="$(< /etc/passwd )"

getlines () {
	local _
	IFS=$'\n' read -d '' "$@" _
}


    zenity --file-selection --multiple --separator=$'\n'
zenity --color-selection --show-palette |
    IFS='(,)' read _ r v b _
print -f '#%x%x%x' $r $v $b
zenity --forms --add-entry={foo,bar,bang} --separator=$'\n' | getlines foo bar bang

