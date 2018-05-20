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
