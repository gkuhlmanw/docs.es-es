---
title: -baseaddress (Opciones del compilador de C#)
ms.date: 07/20/2015
f1_keywords:
- /dllbase
helpviewer_keywords:
- baseaddress compiler option [C#]
- -baseaddress compiler option [C#]
- /baseaddress compiler option [C#]
ms.assetid: ce13c965-dfe4-4433-94f5-63b476e3a608
ms.openlocfilehash: 6ff29a7a204cb8f20f2f67946d5d1ed9c976e7aa
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54694586"
---
# <a name="-baseaddress-c-compiler-options"></a>-baseaddress (Opciones del compilador de C#)
La opción **-baseaddress** permite especificar la dirección base preferida para cargar un archivo DLL. Para obtener más información sobre cuándo y por qué usar esta opción, vea el [blog de Larry Osterman](https://blogs.msdn.microsoft.com/larryosterman/2004/07/06/why-should-i-even-bother-to-use-dlls-in-my-system/).  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
-baseaddress:address  
```  
  
## <a name="arguments"></a>Argumentos  
 `address`  
 La dirección base del archivo DLL. Esta dirección puede especificarse como un número octal, hexadecimal o decimal.  
  
## <a name="remarks"></a>Comentarios  
 La dirección base predeterminada para un archivo DLL se establece mediante Common Language Runtime de .NET Framework.  
  
 Tenga en cuenta que la palabra de orden inferior en esta dirección se redondeará. Por ejemplo, si especifica 0x11110001, se redondeará a 0x11110000.  
  
 Para completar el proceso de firma para un archivo DLL, use SN.EXE con la opción -R.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio  
  
1.  Abra la página **Propiedades** del proyecto.  
  
2.  Haga clic en la página de propiedades de **Compilar**.  
  
3.  Haga clic en el botón **Avanzada** .  
  
4.  Modifique la propiedad **Dirección base del archivo DLL**.  
  
     Para establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.CSharpProjectConfigurationProperties3.BaseAddress%2A>.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.ProcessModule.BaseAddress%2A?displayProperty=nameWithType>
- [Opciones del compilador de C#](../../../csharp/language-reference/compiler-options/index.md)
- [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)
