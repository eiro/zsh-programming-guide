# recursive style

cat-n () {
    local line count=${count?count must be passed as variable};
    read line || return
    echo "$[count++]: $line"
    cat-n
}

# iterative style

cat-n () {
    local line count=${count?count must be passed as variable};
    while {read line} {
        echo "$[count++]: $line"
    }
}

count=5 cat-n < /etc/passwd

