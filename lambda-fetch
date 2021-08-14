#!/bin/bash

# A copy of ufetch with a lambda art
# https://gitlab.com/jschx/ufetch/

# It has one possible flag, -b, to show the big version of the ASCII art.
# If you want it to show up everytime the terminal is opened, you can put
# something like this in your .bashrc (if you use bash):
# ~/lambda-fetch
# If you want the big version:
# ~/lambda-fetch -b
while getopts "b" flag; do
  case $flag in
    b) big=true;;
  esac
done

host="$(hostname)"
os="$(lsb_release -ds)"
kernel="$(uname -sr)"
uptime="$(uptime -p | sed 's/up //')"
# You can uncomment this and use it if you want to
# packages="$(dpkg -l | wc -l)"
shell="$(basename "${SHELL}")"

## UI DETECTION

parse_rcs() {
  for f in "${@}"; do
    wm="$(tail -n 1 "${f}" 2> /dev/null | cut -d ' ' -f 2)"
    [ -n "${wm}" ] && echo "${wm}" && return
  done
}

rcwm="$(parse_rcs "${HOME}/.xinitrc" "${HOME}/.xsession")"

ui='unknown'
uitype='UI'
if [ -n "${DE}" ]; then
  ui="${DE}"
  uitype='DE'
elif [ -n "${WM}" ]; then
  ui="${WM}"
  uitype='WM'
elif [ -n "${XDG_CURRENT_DESKTOP}" ]; then
  ui="${XDG_CURRENT_DESKTOP}"
  uitype='DE'
elif [ -n "${DESKTOP_SESSION}" ]; then
  ui="${DESKTOP_SESSION}"
  uitype='DE'
elif [ -n "${rcwm}" ]; then
  ui="${rcwm}"
  uitype='WM'
elif [ -n "${XDG_SESSION_TYPE}" ]; then
  ui="${XDG_SESSION_TYPE}"
fi

ui="$(basename "${ui}")"

## DEFINE COLORS

if [ -x "$(command -v tput)" ]; then
  c1="$(tput setaf 3)" # yellow
  c2="$(tput setaf 2)" # green
  c3="$(tput setaf 6)" # cyan
  c4="$(tput setaf 4)" # blue
  c5="$(tput setaf 5)" # magenta
  c6="$(tput setaf 1)" # red
  bold="$(tput bold)"  # bold
  reset="$(tput sgr0)"
fi

if [ $big ]; then
# Big lambda (aka Lambdão)
cat <<EOF
${reset}${bold}${c1}   λλλλλ
${bold}${c2}  λλ  λλλ
${bold}${c3}       λλλ          ${USER}@${host}
${bold}${c4}        λλλ         OS: ${reset}${c5}${os}
${bold}${c5}         λλλ        KERNEL: ${reset}${c6}${kernel}
${bold}${c6}        λλλλλ       UPTIME: ${reset}${c1}${uptime}
${bold}${c1}       λλλ λλλ      TERMINAL: ${reset}${c2}${TERM}
${bold}${c2}      λλλ   λλλ     SHELL: ${reset}${c3}${shell}
${bold}${c3}     λλλ     λλλ    ${uitype}: ${reset}${c4}${ui}
${bold}${c4}    λλλ       λλλ
${bold}${c5}   λλλ         λλλ
${bold}${c6}λλλλλ           λλλλλ${reset}
EOF
else
# Smol lambda
cat <<EOF
${reset}${bold}${c1}  λλλ         ${USER}@${host}${reset}
${bold}${c2} λλ λλ        OS: ${reset}${c3}${os}
${bold}${c3}     λλ       KERNEL: ${reset}${c4}${kernel}
${bold}${c4}     λλλ      UPTIME: ${reset}${c5}${uptime}
${bold}${c5}    λλ λλ     TERMINAL: ${reset}${c6}${TERM}
${bold}${c6}   λλ   λλ    SHELL: ${reset}${c1}${shell}
${bold}${c1} λλλ     λλλ  ${uitype}: ${reset}${c2}${ui}${reset}
EOF
fi
