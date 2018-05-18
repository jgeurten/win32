﻿---
Description: 'The MinorVersion property is a value that specifies the minor part of the version number for the fax service.'
ms.assetid: '65e20cef-4f32-403c-84aa-60633dc4e53f'
title: 'FaxServer.MinorVersion property'
---

# FaxServer.MinorVersion property

The **MinorVersion** property is a value that specifies the minor part of the version number for the fax service.

This property is read-only.

## Syntax


```VB
Property MinorVersion As Long
```



## Property value

A **Long** that receives the minor part of the version number (the decimal portion) for the fax service.

## Remarks

The format for the fax service build number is MajorVersion.MinorVersion.MajorBuild.MinorBuild.

## Requirements



|                                     |                                                                                         |
|-------------------------------------|-----------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows XP \[desktop apps only\]<br/>                                             |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/>                                    |
| Header<br/>                   | <dl> <dt>FaxComex.h</dt> </dl>   |
| DLL<br/>                      | <dl> <dt>Fxscomex.dll</dt> </dl> |



## See also

<dl> <dt>

[Visual Basic Example](-mfax-retrieving-server-properties.md)
</dt> <dt>

[**FaxServer**](-mfax-faxserver.md)
</dt> <dt>

[**IFaxServer**](-mfax-faxserver-cpp.md)
</dt> </dl>

 

 



