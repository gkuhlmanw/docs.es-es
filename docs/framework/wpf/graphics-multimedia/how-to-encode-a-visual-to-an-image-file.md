---
title: Procedimiento Codificar un objeto Visual en un archivo de imagen
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- image files [WPF], encoding from visuals
- encoding image formats [WPF]
- visuals [WPF], encoding to an image file
ms.assetid: 2036385b-ea47-4d54-8027-5797f52c8149
ms.openlocfilehash: e8988256d4b7181c5e1af12252ca26e0248d016f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54645228"
---
# <a name="how-to-encode-a-visual-to-an-image-file"></a>Procedimiento Codificar un objeto Visual en un archivo de imagen
En este ejemplo se muestra cómo codificar un <xref:System.Windows.Media.Visual> objeto en un archivo de imagen con un <xref:System.Windows.Media.Imaging.RenderTargetBitmap> y un <xref:System.Windows.Media.Imaging.PngBitmapEncoder>.  
  
## <a name="example"></a>Ejemplo  
 El <xref:System.Windows.Media.DrawingVisual> se crea mediante un <xref:System.Windows.Media.Imaging.BitmapImage> y <xref:System.Windows.Media.FormattedText> que se representa en un <xref:System.Windows.Media.Imaging.RenderTargetBitmap>. El mapa de bits representado, a continuación, se usa para crear un <xref:System.Windows.Media.Imaging.BitmapFrame> que se agrega a la <xref:System.Windows.Media.Imaging.PngBitmapEncoder> para crear un nuevo [!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)] archivo.  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample_Encode.cs#rtbencodeinline1)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample_Encode.vb#rtbencodeinline1)]  
  
 Un <xref:System.Windows.Media.Imaging.PngBitmapEncoder> se usó en este ejemplo, pero los de la clase derivada <xref:System.Windows.Media.Imaging.BitmapEncoder> objetos se podrían haber utilizado para crear el archivo de imagen.  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Media.DrawingContext>
- [Información general sobre imágenes](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)
- [Información general sobre objetos Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)
- [Usar objetos DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)
