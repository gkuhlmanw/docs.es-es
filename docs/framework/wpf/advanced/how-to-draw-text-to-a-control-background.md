---
title: Filtrar Dibujar texto en el fondo de un control
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], drawing text to backgrounds
- text [WPF], drawing to control backgrounds
- drawing [WPF], text to control backgrounds
- backgrounds [WPF], drawing text to
- typography [WPF], drawing text to control backgrounds
ms.assetid: 686d8fba-f61c-4974-a871-c635d67a7f69
ms.openlocfilehash: 9be4eb92021a62baaf6b43198587616d00cc265e
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/30/2019
ms.locfileid: "55259259"
---
# <a name="how-to-draw-text-to-a-controls-background"></a>Filtrar Dibujar texto en el fondo de un control
Puede dibujar texto directamente en el fondo de un control mediante la conversión de una cadena de texto a un <xref:System.Windows.Media.FormattedText> objeto y, a continuación, dibuje el objeto para el control <xref:System.Windows.Media.DrawingContext>. También puede usar esta técnica para dibujar en el fondo de objetos derivados de <xref:System.Windows.Controls.Panel>, tales como <xref:System.Windows.Controls.Canvas> y <xref:System.Windows.Controls.StackPanel>.  
  
 ![Controles mostrando texto como fondo](../../../../docs/framework/wpf/advanced/media/drawtext2background01.png "DrawText2Background01")  
Ejemplo de controles con fondos de texto personalizados  
  
## <a name="example"></a>Ejemplo  
 Para dibujar el fondo de un control, cree un nuevo <xref:System.Windows.Media.DrawingBrush> de objetos y dibujar el texto convertido en el objeto <xref:System.Windows.Media.DrawingContext>. A continuación, asigne el nuevo <xref:System.Windows.Media.DrawingBrush> a la propiedad del control en segundo plano.  
  
 En el ejemplo de código siguiente se muestra cómo crear un <xref:System.Windows.Media.FormattedText> de objetos y dibujar en el fondo de un <xref:System.Windows.Controls.Label> y <xref:System.Windows.Controls.Button> objeto.  
  
 [!code-csharp[DrawTextToControlBackground#DrawTextToControlBackground1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawTextToControlBackground/CSHARP/Window1.xaml.cs#drawtexttocontrolbackground1)]  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Media.FormattedText>
- [Dibujar texto con formato](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)
