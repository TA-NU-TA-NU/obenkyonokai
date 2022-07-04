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

<!-- 変数 -->
{{< note title="Variable" >}}

**変数宣言の仕方**

```powershell
[string]$name="John"
$name

```
{{< /note >}}

<!-- if -->
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