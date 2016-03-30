_cap()
{
    COMPREPLY=()

    local cur prev
    cur="${COMP_WORDS[COMP_CWORD]}"
    prev="${COMP_WORDS[COMP_CWORD-1]}"

    if [ ! -f ./Capfile ];
    then
        return
    fi

    local cap_opt_all
    cap --version | grep 'Capistrano v2.' > /dev/null
    if [ $? -eq 0 ]; then
      cap_opt_all='-v' # Capistrano 2.x
    else
      cap_opt_all='-A' # Capistrano 3.x
    fi

    local opts
    opts=`cap -T ${cap_opt_all} | awk 'BEGIN {x=1}; $x>1 { if($1=="cap") { print $2}}'`
    optscolon=${cur%"${cur##*:}"}

    COMPREPLY=( $(compgen -W "${opts}"  -- ${cur}))

    local i=${#COMPREPLY[*]}
    while [ $((--i)) -ge 0 ]; do
        COMPREPLY[$i]=${COMPREPLY[$i]#"$optscolon"}
    done
}

complete -F _cap cap
