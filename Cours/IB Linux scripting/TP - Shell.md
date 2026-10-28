Exercice pratique: conditions et boucles:

```shell
#!/bin/bash

read -p "Quel est ton nom ? " nom
while [ -z "$nom" ]; do
  echo "Nom vide. Recommence."
  read -p "Quel est ton nom ? " nom
done

echo "Bonjour $nom !"
```


```shell
log() {
    local level="INFO"
    local msg=""

    # Si au moins 2 arguments et que le premier ressemble à un niveau de log
    case "$1" in
        INFO|WARNING|ERROR|DEBUG)
            level="$1"
            shift
            ;;
    esac

    msg="$*"
    timestamp=$(date +%s)  # Format POSIX (timestamp UNIX)
    log_entry="[$timestamp][$level] $msg"

    echo "$log_entry" >> test.log
    echo "$log_entry"
}
```
