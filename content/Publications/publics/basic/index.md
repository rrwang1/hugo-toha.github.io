---
title: Variables
weight: 210
menu:
  sidebar:
    name: Variables
    identifier: variables
    parent: publics
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
