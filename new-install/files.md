# Files

Files to set up.

## ~/.bashrc

```bash
# ~/.bashrc: executed by bash(1) for non-login shells.

# Note: PS1 and umask are already set in /etc/profile. You should not
# need this unless you want different defaults for root.
# PS1='${debian_chroot:+($debian_chroot)}\h:\w\$ '
# umask 022

# You may uncomment the following lines if you want `ls' to be colorized:
#export LS_OPTIONS='--color=auto'
#eval "`dircolors`"
#alias ls='ls $LS_OPTIONS'
#alias ll='ls $LS_OPTIONS -l'
#alias l='ls $LS_OPTIONS -lA'

#force_color_prompt=yes

case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
        # We have color support; assume it's compliant with Ecma-48
        # (ISO/IEC-6429). (Lack of such support is extremely rare, and such
        # a case would tend to support setf rather than setaf.)
        color_prompt=yes
    else
        color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# Some more alias to avoid making mistakes:
# alias rm='rm -i'
# alias cp='cp -i'
# alias mv='mv -i'

alias ls='ls -l -A'
alias myip='/root/./myip.sh'
```

## ~/.vimrc

```bash
syntax on
colorscheme desert
```

## ~/myip.sh

```bash
# Gets the public IP from "ipify.org" and uses "jq" to print out the "ip" key from the JSON data.
# curl https://api.ipify.org?format=json | jq -r '.ip'

json=$(curl https://api.ipify.org?format=json)

# Gets the private address.

private="$(hostname -I)"

printf "\npublic:  "
printf ${json} | jq -r ".ip"
printf "private: "
printf ${private}
printf "\n\n"
```


