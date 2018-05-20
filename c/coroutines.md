
If pipes on your system are bidirectional (as they are on Solaris 11 and some
BSDs at least, but not Linux):

cmd1 <&1 | cmd2 >&0
