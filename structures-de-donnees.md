listes

dispatch player doo set

foo=bar
eval "$1='$(mktemp -d)'"

doo=$( mktemp -d doo-XXX )
<<< doo >> $doo/uid
<<< doo >> $doo/uid2
print $doo

/home/mc/www/e/zsh-programming
index.md
structures-de-donnees.md
zsh-from-perl.md

z=$(<<-E
	'love is all'
	"$USER"
        u{a,g}
        *
E
)
echo $z

echo hello world
pwd
ls
ls /
ls .
ls -A .

echo io
echo $z

$players/$d 
oo/$bio <<

{ read a ; read b; read c; } <<< 'aaa
bbb
ccc
'
echo "$a -> $b -> $c"


( player doo

)



sed '/^doo$/d' $players



my@ users=(
    'display Marc\ Chantreux login mc'
    'display John\ Doe       login jd'
)

@ ($users) {
    my% u=(${(z)it})
    l $u[display]
}

contact=dave.null@phear.org
echo user: ${contact%@*}
echo org : ${contact#*@}

cnx_info_parse () {
    local it=${1:-it}
    case $it {
        (*@*:*) user=${it%@*} host=${${it#*@}%:*} port=${it#*:} ;;
        (*:*)   user=         host=${it%:*}       port=${it#:*} ;;
        (*@*)   user=${it%@*} host=${it#*@}       port=         ;;
        (*)     user=         host=$it            port=         ;;
    }
}

cnx_info_parse () {
    my@ match mbegin mend
    local it=${1:-it}
    case $it {
        ((#b)(*)@(*):(*)) user=$match[1] host=$match[2] port=$match[3] ;;
        ((#b)(*):(*))     user=          host=$match[1] port=$match[2] ;;
        ((#b)(*)@(*))     user=$match[1] host=$match[2] port=          ;;
        (*)               user=          host=$it       port=          ;;
    }
}

cnx_info_dump () {
    local user host port
    cnx_info_parse $1
    echo "$1 =>" user=$user host=$host port=$port
}

@ ( domination@world:22
    domination@world
    world:22
) cnx_info_dump $it

exit
# deal with data structures

# symbolic references

my% server=( key ssh_key_django )

my% ssh_key_django=(
    private django
    public  django.pub
    desc    'django ssh service key')

echo ${server[key]}
echo ${${(P)server[key]}[public]}

# serialize your data

my% contact=( user dave.null org phear.org )

contact=dave.null@phear.org
${contact#@*}

## files

"we have datastructures called files" quote

# echo ${${(P)server[key]}[author]}
# # echo ${(Pv)server[key][author]}

    directors=( director{1,2,3} )
    local -A $directors

    director1=( ssh ha@d1.example.com desc 'director 1' )
    director2=( ssh ha@d2.example.com desc 'director 2' )
    director3=( ssh ha@d3.example.com desc 'director 3' )

    for it ( $directors )
        ssh ${${(P)it}[ssh]} :

