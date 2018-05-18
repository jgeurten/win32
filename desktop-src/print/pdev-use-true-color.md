﻿---
Description: 'The PDEV\_USE\_TRUE\_COLOR structure indicates whether the output color space should be color or grayscale.'
ms.assetid: '75ffe04a-4d77-4486-8fc7-35b0b6144b99'
title: 'PDEV\_USE\_TRUE\_COLOR structure'
---

# PDEV\_USE\_TRUE\_COLOR structure

The PDEV\_USE\_TRUE\_COLOR structure indicates whether the output color space should be color or grayscale.

## Syntax


```C++
typedef struct _PDEV_USE_TRUE_COLOR {
  BOOL bUseTrueColor;
} PDEV_USE_TRUE_COLOR;
```



## Members

<dl> <dt>

**bUseTrueColor**
</dt> <dd>

Specifies whether the PostScript output should be in color mode or in monochrome/grayscale mode. If **TRUE**, output is in color. If **FALSE**, output is monochrome/grayscale.

</dd> </dl>

## Remarks

This structure is available in Windows XP and later.

The *pBuf* parameter of the [**IPrintOemPS2::GetPDEVAdjustment**](iprintoemps2-getpdevadjustment.md) method can point to a structure of this type.

A plug-in can use this flag to turn color output on or off for Pscript5 printer output data. If the plug-in chooses to not change the current setting, it can simply return S\_FALSE.

## Requirements



|                   |                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------|
| Header<br/> | <dl> <dt>Printoem.h (include Prcomoem.h)</dt> </dl> |



## See also

<dl> <dt>

[**IPrintOemPS2::GetPDEVAdjustment**](iprintoemps2-getpdevadjustment.md)
</dt> </dl>

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20PDEV_USE_TRUE_COLOR%20structure%20%20RELEASE:%20%285/12/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default.aspx. "Send comments about this topic to Microsoft")




