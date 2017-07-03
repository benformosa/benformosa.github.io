---
published: false
---
I keep a number of physical sticky notes and cheatsheets around my desk at work.

## Useful commands
### Create MediaWiki Table from csv
Requires `python-tabulate`
```bash
python -m tabulate -1 -f mediawiki /path/to/input/file | tr -s '[:blank:]' | sed 's/ \([|!]\)/\n\1/g' | sed 's/\([|!]\)\+/\1/g'
```
### vim
`C-w H`
: vertical split
`C-w K`
: horizontal split
`:w !sudo tee %`
: save as root