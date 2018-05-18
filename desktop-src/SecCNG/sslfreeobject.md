---
Description: 'Frees a key, hash, or provider object.'
ms.assetid: '73fa0a08-4654-4515-bdb2-9951936b689a'
title: SslFreeObject function
---

# SslFreeObject function

The **SslFreeObject** function frees a key, hash, or provider object.

## Syntax


```C++
SECURITY_STATUS WINAPI SslFreeObject(
  _In_�NCRYPT_HANDLE hObject,
  _In_�DWORD ��������dwFlags
);
```



## Parameters

<dl> <dt>

*hObject* \[in\]
</dt> <dd>

The handle of the object to free.

</dd> <dt>

*dwFlags* \[in\]
</dt> <dd>

This parameter is reserved for future use.

</dd> </dl>

## Return value

If the function succeeds, it returns zero.

If the function fails, it returns a nonzero error value.

Possible return codes include, but are not limited to, the following.



| Return code/value                                                                                                                                                       | Description                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| <dl> <dt>**NTE\_INVALID\_HANDLE**</dt> <dt>0x80090026L</dt> </dl>    | An internal handle is not valid.<br/>  |
| <dl> <dt>**STATUS\_INVALID\_HANDLE**</dt> <dt>0xC0000008L</dt> </dl> | The provided handle is not valid.<br/> |



�

## Requirements



|                                     |                                                                                          |
|-------------------------------------|------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista \[desktop apps only\]<br/>                                           |
| Minimum supported server<br/> | Windows Server�2008 \[desktop apps only\]<br/>                                     |
| Header<br/>                   | <dl> <dt>Sslprovider.h</dt> </dl> |
| DLL<br/>                      | <dl> <dt>Ncrypt.dll</dt> </dl>    |



�

�



