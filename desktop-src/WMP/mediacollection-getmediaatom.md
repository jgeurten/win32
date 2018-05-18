---
title: MediaCollection.getMediaAtom method
description: The getMediaAtom method retrieves the index at which a specified attribute resides within the set of available attributes.
ms.assetid: '22024108-398e-4a05-b5ed-311583c69497'
keywords: ["getMediaAtom method Windows Media Player", "getMediaAtom method Windows Media Player , MediaCollection class", "MediaCollection class Windows Media Player , getMediaAtom method"]
topic_type:
- apiref
api_name:
- MediaCollection.getMediaAtom
api_location:
- wmp.dll
api_type:
- COM
---

# MediaCollection.getMediaAtom method

The **getMediaAtom** method retrieves the index at which a specified attribute resides within the set of available attributes.

## Syntax


```JScript
retVal = MediaCollection.getMediaAtom(
  attribute
)
```



## Parameters

<dl> <dt>

*attribute* \[in\]
</dt> <dd>

**String** containing the attribute name. For information about the attributes supported by Windows Media Player, see the Windows Media Player [Attribute Reference](attribute-reference.md).

</dd> </dl>

## Return value

This method returns a **Number** (**long**).

## Remarks

The index number retrieved with this method can be passed to the *Media*.**getItemInfoByAtom** method to access attribute values. This technique is generally more efficient when working with large playlists than accessing an attribute value by name through *Media*.**getItemInfo** or *Media*.**getItemInfoByType**.

To use this method, read access to the library is required. For more information, see [Library Access](library-access.md).

## Requirements



|                    |                                                                                    |
|--------------------|------------------------------------------------------------------------------------|
| Version<br/> | Windows Media Player version 7.0 or later.<br/>                              |
| DLL<br/>     | <dl> <dt>Wmp.dll</dt> </dl> |



## See also

<dl> <dt>

[**Media.getItemInfo**](media-getiteminfo.md)
</dt> <dt>

[**Media.getItemInfoByAtom**](media-getiteminfobyatom.md)
</dt> <dt>

[**Media.getItemInfoByType**](media-getiteminfobytype.md)
</dt> <dt>

[**MediaCollection Object**](mediacollection-object.md)
</dt> <dt>

[**Settings.mediaAccessRights**](settings-mediaaccessrights.md)
</dt> <dt>

[**Settings.requestMediaAccessRights**](settings-requestmediaaccessrights.md)
</dt> </dl>

�

�




