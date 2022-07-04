---
title: Powershell Variables
weight: 210
menu:
  notes:
    name: Variables
    identifier: notes-powershell
    parent: Powershell
    weight: 10
---

<!-- Variable -->
{{< note title="Variable" >}}

**変数宣言の仕方**

```powershell
[string]$name="John"
$name

```
{{< /note >}}

<!-- If -->
{{< note title="If" >}}
**if文のサンプル**
```powershell
[boolean]$foo=$true
if($foo){
  write-host "this is true!"
}else{
  write-host "this is false!"
}
```
{{< /note >}}