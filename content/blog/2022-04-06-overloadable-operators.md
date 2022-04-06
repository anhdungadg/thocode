---
title: Overloadable operators
date: 2022-04-06T09:17:09.657Z
tags:
  - C#
  - newbie
draft: false
---
C# cho phép dùng operator với Class, Struct

```csharp
public struct Complex
        {
            public double Real { get; set; }
            public double Imaginary { get; set; }

            public static Complex operator +(Complex c1, Complex c2)
            {
                return new Complex
                {
                    Real = c1.Real + c2.Real,
                    Imaginary = c1.Imaginary + c2.Imaginary
                };
            }
        }
```



**Nhiếp Phong**