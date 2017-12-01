---
title: "Cómo: abrir un cuadro de mensaje"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- message boxes [WPF], opening
- opening message boxes [WPF]
ms.assetid: acaad17f-af43-4eca-a004-f1c9e7c6f292
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 302a3cd34d90d47e38af1bbeaadca7e777a26395
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-open-a-message-box"></a><span data-ttu-id="0c81b-102">Cómo: abrir un cuadro de mensaje</span><span class="sxs-lookup"><span data-stu-id="0c81b-102">How to: Open a Message Box</span></span>
<span data-ttu-id="0c81b-103">Este ejemplo muestra cómo abrir un cuadro de mensaje.</span><span class="sxs-lookup"><span data-stu-id="0c81b-103">This example shows how to open a message box.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0c81b-104">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0c81b-104">Example</span></span>  
 <span data-ttu-id="0c81b-105">Un cuadro de mensaje es un cuadro de diálogo modal prefabricado para mostrar información a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0c81b-105">A message box is a prefabricated modal dialog box for displaying information to users.</span></span> <span data-ttu-id="0c81b-106">Se abre un cuadro de mensaje mediante una llamada a estático <xref:System.Windows.MessageBox.Show%2A> método de la <xref:System.Windows.MessageBox> clase.</span><span class="sxs-lookup"><span data-stu-id="0c81b-106">A message box is opened by calling the static <xref:System.Windows.MessageBox.Show%2A> method of the <xref:System.Windows.MessageBox> class.</span></span> <span data-ttu-id="0c81b-107">Cuando <xref:System.Windows.MessageBox.Show%2A> es llama, se pasa el mensaje mediante un parámetro de cadena.</span><span class="sxs-lookup"><span data-stu-id="0c81b-107">When <xref:System.Windows.MessageBox.Show%2A> is called, the message is passed using a string parameter.</span></span> <span data-ttu-id="0c81b-108">Varias sobrecargas de <xref:System.Windows.MessageBox.Show%2A> le permiten configurar cómo aparecerá un cuadro de mensaje (consulte <xref:System.Windows.MessageBox>).</span><span class="sxs-lookup"><span data-stu-id="0c81b-108">Several overloads of <xref:System.Windows.MessageBox.Show%2A> allow you to configure how a message box will appear (see <xref:System.Windows.MessageBox>).</span></span>  
  
 [!code-csharp[MessageBoxSnippets#MessageBoxShow1CODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MessageBoxSnippets/CSharp/Show1Window.xaml.cs#messageboxshow1code)]
 [!code-vb[MessageBoxSnippets#MessageBoxShow1CODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MessageBoxSnippets/visualbasic/show1window.xaml.vb#messageboxshow1code)]  
  
## <a name="see-also"></a><span data-ttu-id="0c81b-109">Vea también</span><span class="sxs-lookup"><span data-stu-id="0c81b-109">See Also</span></span>  
 [<span data-ttu-id="0c81b-110">Ejemplo de cuadro de mensajes</span><span class="sxs-lookup"><span data-stu-id="0c81b-110">MessageBox Sample</span></span>](http://go.microsoft.com/fwlink/?LinkID=160023)