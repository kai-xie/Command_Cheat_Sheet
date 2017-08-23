# Linux

[TOC]

## Frequently Used

### tar

tar 
  **Option** |	**Description**
  :--- | :---
`tar -cf archive.tar foo bar`  | # Create archive.tarfrom files foo and bar.
`tar -tvf archive.tar       `  | # List all files inarchive.tar verbosely.
`tar -xf archive.tar        `  | # Extract all filesfrom archive.tar.
`tar -cavf data.tar.gz --exclude=/data/web/aaa --exclude=/data/web/bbb /data/web/` |
`tar cvzf data.tar.gz --exclude-from /data/excludefile  /data/web/` | # in the excludefile: <br> */data/web/aaa* <br> */data/web/bbb*  <br />

