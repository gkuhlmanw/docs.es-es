---
title: 'Cómo: Modificar la tipografía de texto'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- setting Typography attributes [WPF]
- Typography attribute [WPF], setting
ms.assetid: 19a3b49b-60a2-4c11-a786-e26b4c965588
ms.openlocfilehash: f04c873e542ad02c1d2a20b770ded4464af7a6d8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54645410"
---
# <a name="how-to-alter-the-typography-of-text"></a>Cómo: Modificar la tipografía de texto
El ejemplo siguiente muestra cómo establecer el <xref:System.Windows.Documents.TextElement.Typography%2A> atributo, mediante <xref:System.Windows.Documents.Paragraph> como elemento de ejemplo.  
  
## <a name="example"></a>Ejemplo  
 [!code-xaml[TextElementSnippets#_TextElement_TypogXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 En la ilustración siguiente, se muestra cómo se representa este ejemplo.  
  
 ![Captura de pantalla: Texto con tipografía modificada](../../../../docs/framework/wpf/advanced/media/textelement-typog.png "TextElement_Typog")  
  
 En cambio, en la siguiente ilustración se muestra cómo se representa un ejemplo similar con propiedades tipográficas predeterminadas.  
  
 ![Captura de pantalla: Texto con tipografía modificada](../../../../docs/framework/wpf/advanced/media/textelement-typog-default.png "TextElement_Typog_Default")  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo establecer el <xref:System.Windows.Controls.TextBox.Typography%2A> propiedad mediante programación.  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
## <a name="see-also"></a>Vea también
- [Información general sobre documentos dinámicos](../../../../docs/framework/wpf/advanced/flow-document-overview.md)
