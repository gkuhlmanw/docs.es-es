---
title: '##Const (directiva) (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.#Const
- '#vb.Const'
- '#Const'
helpviewer_keywords:
- '#Const directive'
- conditional compilation [Visual Basic], directives
- Const directive (#Const)
- Visual Basic compiler, compiler directives
- constants [Visual Basic], Const directive
- constants [Visual Basic], declaring
- Const statement [Visual Basic], directive (#Const)
- 'declaring constants [Visual Basic], #const directive'
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
ms.openlocfilehash: 7e855f76a0fa8e6c06fd557a944c518641415f09
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54710604"
---
# <a name="const-directive"></a>#Const (Directiva)
Define las constantes de compilador condicionales para Visual Basic.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
#Const constname = expression  
```  
  
## <a name="parts"></a>Elementos  
 `constname`  
 Obligatorio. Nombre de la constante que se está definida.  
  
 `expression`  
 Obligatorio. Literal, otra constante de compilación condicional o cualquier combinación que incluya operadores aritméticos o lógicos, excepto `Is`.  
  
## <a name="remarks"></a>Comentarios  
 Constantes de compilador condicionales son siempre privadas en el archivo en el que aparecen. No se puede crear constantes de compilación público con el `#Const` directiva; puede crear solo en la interfaz de usuario o con el `/define` opción del compilador.  
  
 Puede usar solo constantes de compilador condicionales y literales en `expression`. Uso de una constante estándar definida con `Const` produce un error. Por el contrario, puede usar constantes definidas con el `#Const` palabra clave para la compilación condicional. Las constantes pueden también no estén definidas, en cuyo caso su valor `Nothing`.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usa la directiva `#Const`.  
  
 [!code-vb[VbVbalrConditionalComp#3](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/const-directive_1.vb)]  
  
## <a name="see-also"></a>Vea también
- [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [#If...Then...#Else (directivas)](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [Const (instrucción)](../../../visual-basic/language-reference/statements/const-statement.md)
- [Compilación condicional](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [If...Then...Else (instrucción)](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
