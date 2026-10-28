
```
if command; then
# command was successful
fi
if ! command; then
# command was unsuccessful
fi
```

```
let result="4 * 5"
echo $result

ou

result=$((5 * 5))
echo $result

ou

result=$(expr 5 + 505)
echo $result
```

```
cat << EOF
Black Hat Bash
by No Starch Press
EOF
```

```
sed 's/Mozilla/Godzilla/g' log.txt
sed '1d' log.txt #delete premiere ligne
sed '$d' log.txt #delete derniere ligne
sed '5,7d' log.txt #delete 5 et 7
sed -n '2,15 p' log.txt #delete 2 a 15

When you pass sed the -i argument, it will make the changes to the file
itself rather than create a modified copy
```

unset VARIABLE
ps
grep
regex
sed
mettre sa commande dans le path