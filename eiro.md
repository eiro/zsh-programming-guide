% Notes zsh

# scalars

are nothing but strings

    echo 3 + 3

are nothing but strings

## Datastructures

### Associations

### from line records to associations

how to read this line in an association? 

     mc:x:1002:100:Marc Chantreux,,,:/home/mc:/bin/zsh

the perl version would be

    my %user;
    @user{qw( login x uid gid gecos home shell )} = split /:/, $line

easier to maintain if you store the keys in a separate list

    my @attrs = qw( login x uid gid gecos home shell );
    my %user;
    @user{@attrs} = split /:/, $line

the zsh version isn't longuer

    my% user
    entry="$( getent passwd mc )"
    attrs=( login x uid gid gecos home shell )
    IFS=: read user\[$^attrs] <<< $entry

got it? no? so hack it. the expanded version is

    my% user
    entry="$( getent passwd mc )"

    IFS=: read  \
    user[login] \
    user[x]     \
    user[uid]   \
    user[gid]   \
    user[gecos] \
    user[home]  \
    user[shell] <<< $entry

but we can use brace expansions here

    # /!\ this doesn't work because zsh recognize a glob 
    #     and wants to expand it

    user[{login,x,uid,gid,gecos,home,shell}] <<< $entry

you're one caracter left

    user\[{login,x,uid,gid,gecos,home,shell}] <<< $entry

now you need to put the keys in an array

    attrs=( login x login x uid gid gecos home shell )
    user\[$^attrs] <<< $entry

### serialize an association

see http://www.zsh.org/mla/users/2012/msg00005.html. note that it also work
with P. so we can imagine a `pp` (ruby "pretty print") as

    pp () {
        case ${(Pt)1} {
            (array)       print "$1=(${(Pq-)1})"
            (association) print "my% $1=(${(P@kvq-)1})" ;;
            (*)           ... ;;
        }
    }

### serialize a list of variables

    attrs=( login x uid gid gecos home shell )
    getent passwd mc | IFS=: read $attrs
    eval "print \$${(j,:$,)attrs}"

### awk alike functions

    getent passwd | read -A argv
    print $1 # gets the login

# zsh aliases i'm happy about

years ago, i was very skeptical when i saw this

    alias g="git"

in the
[Franck Cuny's .bashrc](https://github.com/franckcuny/home/blob/master/bashrc).
I argued it wasn't worth to alias a command with such a short name.
Franck just replied "it's faster" and this chat was as short as a
smalltalk.

Months later, i thought to myself it was worth to add 1 line in my `.zshenv`
to give it a try. and it was worth! so f`******` worth!

Since then, i have a simple rule: if

* the average number of use is more than 3times/h (every day)
* the shorthand shorter or equals 1/3 the long of the original

it deserve a shorthand! so mine are

    alias v=vim
    alias z=zsh
    alias s=ssh
    alias l='print -l'
    sz () { ssh "$@" zsh } 
    alias g=git
    alias @='for it'
    alias @-='while {read it}'
    alias %='for k v'

`~/.ssh/config` also have some shorthands, for example 

    host gh
    hostname github.com
    user git

    host w
    hostname www.mycompagny.example.com
    user www-data

    host db
    hostname www.mycompagny.example.com
    user operator

so now i can write things like

    l "select * from table" | s db | v -

so i launch an sql query using the default database configured in 
`db@hostname www.mycompagny.example.com/.my.cnf` and get the result
in a vim buffer, ready to be edited.

if you're comming from langages like `perl`, `livescript`, `groovy` or
any of those langages coming with partial applications or context variables,
you miss `it` (`$_` in `perl`). don't you? so just use it.

both

    seq 10|@- { l "$it * 3 = $[it*3]" }
    @ ( {1..10} ) l "$it * 3 = $[it*3]"

will produce

    1 * 3 = 3
    2 * 3 = 6
    3 * 3 = 9
    4 * 3 = 12
    5 * 3 = 15
    6 * 3 = 18
    7 * 3 = 21
    8 * 3 = 24
    9 * 3 = 27
    10 * 3 = 30

thanks to variable interpolations, the equivalent of `it` in livescript (or `_
prototype` in perl) can be written as `${1:=$it}`.

    remote-date () { s ${1:=$it} date }
    @ ($servers) remote-date

i also have more `perl inspired` features including ̀ warn`, `die` and the
yada-yada operator (`...`):

    warn () {
            LAST_ERROR=$? 
            print -u2 "$*"
            return $LAST_ERROR
    }
    die () {
            LAST_ERROR=$? 
            print -u2 "$*"
            exit $LAST_ERROR
    }
    alias error=warn "in $0 line $LINENO:"
    alias ...='{error Unimplemented; return 255}'

a more complete example is

    # server_exists () { grep -q ${1-${it?name of the server} ~/.servers }
    # @ ( srv-{web,db,mq} ) { server_exists ||error "$it doesn't exist"}

    in zsh line 2: srv-web doesn't exist
    in zsh line 2: srv-db doesn't exist

    # server_exists || ...

        in zsh line 1: Unimplemented

some of those ideas could be shared using
using [uze](http://zsh-uze.github.io/)).

# piping from vim

from vim, visually select your sql query and type

    '<,'>!s db-server mysql

since each results are data to write the next query or command, i spend much of
my time in vim now.






