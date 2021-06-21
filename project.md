<!--
author:   Mark Jacob
email:    Mark.Jacob@iuz.tu-freiberg.de
version:  0.0.1
language: en
narrator: UK English Female

import: https://github.com/liascript/CodeRunner

comment:  This document is a test ...

dark:     true

mode: Presentation

-->

# test

```csharp        FirstStructExample
using System;
public class Program
{
  static void Main(string[] args){
      Console.WriteLine("Hello world");
  }
}
```
@LIA.eval(`["main.cs"]`, `mono main.cs`, `mono main.exe`)

```Python3    penis
for i in range(10):
  print("Hallo Welt", i)
```
@LIA.eval(["main.py"], python3 -m compileall ., python3 main.py)


## video

*Definitely not a Rick Roll!*
!?[alt-text](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

## table

| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| Text     | Text     | Text     |


## Lia-Script

Please click on the right-pointing arrow below the photo to start the course.

    --{{1}}--
Welcome to this LiaScript course designed to give you a taster of what we can do in Freiberg. LiaScript is being developed here at the Department of Computer Science. Click on the right-pointing arrow below the photo of our campus to move to the next page.

![image alt](https://tu-freiberg.de/sites/default/files/imagecache/Bereichsgrafik/media/universitaet-4796/bildergalerien/banner_universitaet.jpg)
