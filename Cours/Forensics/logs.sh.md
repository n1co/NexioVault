```shell
#!/bin/bash

FILE="ch13.txt"
COUNT=0
FLAG_B=""
FLAG=""

for SECOND in $(cat "${FILE}" | tr ' ' ':' | cut -f7 -d':'); do
    if [ $COUNT -eq 0 ]; then
        LAST_SECOND=$SECOND
        COUNT=$((COUNT + 1))
        continue
    fi

    if [ $SECOND -lt $LAST_SECOND ]; then
        LAP_S=$((60 + SECOND - LAST_SECOND))
    else
        LAP_S=$((SECOND - LAST_SECOND))
    fi

    if [ $((COUNT % 4)) -eq 0 ]; then
        HF=1
    else
        HF=0
    fi

    case "$LAP_S" in
        0) [ $HF -ne 1 ] && LAST_BIT="00" || LAST_BIT="" ;;
        2) [ $HF -ne 1 ] && LAST_BIT="01" || LAST_BIT="0" ;;
        4) [ $HF -ne 1 ] && LAST_BIT="10" || LAST_BIT="1" ;;
        6) LAST_BIT="11" ;;
    esac

    FLAG_B="${FLAG_B}${LAST_BIT}"

    if [ $((COUNT % 4)) -eq 0 ]; then
        FLAG="${FLAG}$(printf "\\$(printf '%03o' "$((2#$FLAG_B))")")"
        FLAG_B=""
    fi

    LAST_SECOND=$SECOND
    COUNT=$((COUNT + 1))
done

echo "$FLAG"

```
