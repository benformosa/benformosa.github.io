---
layout: default
title: Sticky notes and cheat sheets
categories:
  - blog
tags:
  - organisation
  - notekeeping
---

Even though I am a very strong proponent of a paper-free workflow, I keep a number of physical sticky notes and cheatsheets around my desk at work. These are usually quick reminders of useful things I use infrequently.

## Useful commands
### Vim
`C-w H`
: Vertical split

`C-w K`
: Horizontal split

`:w !sudo tee %`
: Save as root

### Git
`git diff --color-words=.`
: Highlight changed characters, instead of whole lines

`git pull --rebase`
: Pull in ff commits without having to do a merge commit

### Bash
`C-x C-e`
: Edit current command

### Misc
`openssl x509 -in <CERT> -noout -text`
: View a digital certificate

#### Create MediaWiki Table from csv
This one isn't on a sticky note yet, but I wanted to record it somewhere. I'm constantly using [Tables Generator](http://www.tablesgenerator.com/mediawiki_tables) when working on the wiki, but who knows where it's sending my data.
Requires `python-tabulate`
```bash
python -m tabulate -1 -f mediawiki /path/to/input/file | tr -s '[:blank:]' | sed 's/ \([|!]\)/\n\1/g' | sed 's/\([|!]\)\+/\1/g'
```

## Cheat Sheets
* [PacketLife.net IPv4 Subnetting](http://media.packetlife.net/media/library/15/IPv4_Subnetting.pdf)
* [Intercal character set](https://3e8.org/pub/intercal.pdf) - page 22.

## Advice to myself
> It's not DNS  
> There's no way it's DNS  
> It was DNS

[SSBroski](https://www.reddit.com/r/sysadmin/comments/4oj7pv/network_solutions_haiku/d4czk91/)
