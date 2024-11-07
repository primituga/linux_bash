# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# User specific environment
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]; then
    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
fi
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
if [ -d ~/.bashrc.d ]; then
    for rc in ~/.bashrc.d/*; do
        if [ -f "$rc" ]; then
            . "$rc"
        fi
    done
fi
unset rc

####################################################################################################################################
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

mkdir -p envdebug && env | sort > ~/envdebug/bashrc.`date +%s`

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=10000
HISTFILESIZE=20000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
#[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
force_color_prompt=yes

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

# The following block is surrounded by two delimiters.
# These delimiters must not be modified. Thanks.
# START KALI CONFIG VARIABLES
PROMPT_ALTERNATIVE=twoline
NEWLINE_BEFORE_PROMPT=yes
# STOP KALI CONFIG VARIABLES

if [ "$color_prompt" = yes ]; then
    # override default virtualenv indicator in prompt
    VIRTUAL_ENV_DISABLE_PROMPT=1
#####################################
#for COLOR in {1..255}; do echo -en "\e[38;5;${COLOR}m${COLOR} \e[33;0m"; done; echo;
    black='\[\033[38;4;40m\]'  #black background
    red='\[\033[38;5;196m\]'  #red
    green='\[\033[38;5;46m\]' #green
    blue='\[\033[38;5;33m\]'  #blue
    orange='\[\033[38;5;208m\]'
    bolt='\[\033[1m\]'
    underline='\[\033[21m\]'
    resetText='\[\033[0m\]'
    white='\[\033[38;5;254m\]'
    grey1='\[\033[38;5;241m\]'
    grey2='\[\033[38;5;254m\]'
    blink='\[\033[33;5;254m\]'
    info_color=$green 
    prompt_color=$blue
    prompt_user=$orange$bolt
    #prompt_symbol=㉿
    #prompt_symbol=🟢
    prompt_symbol=🐧
#######################################
    if [ "$EUID" -eq 0 ]; then # Change prompt colors for root user
        prompt_user=$underline$red$bolt
        prompt_color=$underline$red
        info_color=$red
        prompt_symbol=$blink💀$resetText$bolt
    fi
    PS1=''$resetText'
'$grey1'╭'$prompt_user'\u'$white''$prompt_symbol''$prompt_color'\h'$resetText''$grey1' | \d, \t:
'$grey1'├'$info_color'[\w]'$resetText'
'$grey1'╰\!'$grey2'»'$resetText' '
    unset black
    unset red
    unset green
    unset blue
    unset orange
    unset bolt
    unset underline
    unset resetText
    unset white
    unset grey1
    unset grey2
    unset info_color
    unset prompt_color
    unset prompt_user
    unset prompt_symbol
    unset blink
fi
unset color_prompt force_color_prompt

[ "$NEWLINE_BEFORE_PROMPT" = yes ] && PROMPT_COMMAND="PROMPT_COMMAND=echo"

# enable color support of ls, less and man, and also add handy aliases

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
black='\033[38;4;40m'
red='\033[38;5;196m'
green='\033[38;5;46m'
blue='\033[38;5;33m'
orange='\033[38;5;208m'
bolt='\033[1m'
underline='\033[21m'
resetText='\033[0m'
white='\033[38;5;254m'
grey1='\033[38;5;241m'
grey2='\033[38;5;254m'
blink='\033[33;5;254m'
#type -a     descreve o comando  
alias ll='ls -l'
alias la='ls -A'
alias l='ls -CF'
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias sstop='swapoff && sudo killall gnome-software || true && sudo killall gitlab-runner || true && sudo killall /usr/libexec/evolution-* || true && sudo killall /usr/libexec/evolution-data-server/* || true && sudo killall packagekitd || true && sudo killall python3 || true && sstop2'
alias sstop2='swapoff && sudo killall mysqld  || true && sudo killall gnome-software  || true && sudo systemctl stop docker.socket  || true && sudo systemctl stop docker.socket  || true && sudo killall containerd  || true && sudo killall gitlab-runner  || true && sudo killall /usr/libexec/evolution-*  || true && sudo killall /usr/libexec/evolution-data-server/* || true '
alias up='
echo -e "$blue sudo dnf update $white" && sudo dnf update --best --allowerasing -y
echo -e "$blue upgrade --refresh $white" && sudo dnf upgrade --refresh -y
echo -e "$blue upgrade $white" && sudo dnf upgrade -y
echo -e "$blue snap refresh $white" && sudo snap refresh
echo -e "$blue flatpak update --system $white" && flatpak update --system -y
echo -e "$blue flatpak update $white" && sudo flatpak update -y
echo -e "$blue groupupdate core $white" && sudo dnf groupupdate core -y
echo -e "$blue install kernel-devel-matched $white" && sudo dnf install kernel-devel-matched
echo -e "$blue autoremove $white" && sudo dnf autoremove -y
echo -e "$blue dnf check $white" && sudo dnf check
#echo -e "$blue winetricks --self-update $white" && sudo winetricks --self-update
#echo -e "$blue freshclam $white" && sudo freshclam || true'
alias upall='up && sudo dracut --force --no-hostonly && sudo fwupdmgr refresh --force && sudo fwupdmgr get-updates && sudo fwupdmgr update && sudo fwupdmgr upgrade'
alias clean='sudo dnf autoremove -y && sudo dnf clean all && sudo dnf clean metadata && sudo dnf check && flatpak uninstall --unused --delete-data -y && sudo rm -rfv /var/tmp/flatpak-cache-* && rm -rfv ~/.cache/flatpak/* && sudo flatpak repair'
alias fixkernel='sudo dracut --force --no-hostonly'
alias asciicolors='for COLOR in {1..255}; do echo -en "\e[38;5;${COLOR}m${COLOR} \e[33;0m"; done; echo;'
alias arduino_usb='sudo chmod 666 /dev/ttyUSB0'
alias arduino_lil='sudo chmod 666 /dev/ttyACM0'
alias swap0='sudo sysctl vm.swappiness=0'
alias swap60='sudo sysctl vm.swappiness=60'
alias swapon='free -h && sudo swapon -a && swap60'
alias swapoff='free -h && sudo swapoff -a && swap0'
alias limpar='sudo sysctl vm.drop_caches=3 && sudo journalctl --vacuum-size=100M'
alias montarext='if [ ! -d /home/primifed/mountEXT1.5 ]; then
  mkdir -p /home/primifed/mountEXT1.5;
fi
sudo mount -t nfs 172.173.174.92:/ext1.5 ~/mountEXT1.5 && echo -e "$red NFS montado em ~/mountEXT1.5 "'
alias montarsd='if [ ! -d /home/primifed/mountSD ]; then
  mkdir -p /home/primifed/mountSD;
fi
sudo mount -t nfs 172.173.174.92:/sd ~/mountSD && echo -e "$red NFS montado em ~/mountSD"'
alias desmontarext='sudo umount -t nfs 172.173.174.92:/ext1.5 ~/mountNFS'
alias desmontarsd='sudo umount -t nfs 172.173.174.88:/sd ~/mountSD'
alias reload='source ~/.bashrc'
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias ll='ls -al --color=auto'
alias du='du -ch --max-depth=1'
alias mem='free -h'
alias f='find . -typef -name'
alias grep='grep --color=auto -i'
alias hgrep='history|grep'
alias chown='chown --preserve-root'
alias chmod='chmod --preserve-root'
alias ports='sudo ss -tulanp'
alias status='sudo systemctl status'
alias restart='sudo systemctl restart'
alias please='sudo !!'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi


