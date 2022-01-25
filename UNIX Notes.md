# Useful UNIX
-w - adds a wait to update in your cmd (kubectl get pod ... -w)

# Useful GREP
- -i - ignore casing (camel casing, etc.)
- -a - everything before the match
- -C - surronding
- -(10) - number of lines
  - kubectl explain pod.spec | grep -i -C 10 nodeselector
