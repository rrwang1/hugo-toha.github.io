---
title: Conference
weight: 210
menu:
  sidebar:
    name: Conference
    identifier: notes-bash-conference
    parent: notes-bash
    weight: 10
---
<!-- Variable -->

{{< note title="Variable" >}}

```bash
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}
```

{{< /note >}}

<!-- Condition -->

{{< note title="Condition" >}}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

{{< /note >}}
