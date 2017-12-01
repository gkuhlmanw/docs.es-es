---
title: ICorDebugValue2 (Interfaz)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugValue2
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugValue2
helpviewer_keywords: ICorDebugValue2 interface [.NET Framework debugging]
ms.assetid: 3ff2ad2a-da5a-461b-8627-1a8eba49df9c
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: f74a90952c6ac780c53441af472faeb999febbb2
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugvalue2-interface"></a><span data-ttu-id="b32f8-102">ICorDebugValue2 (Interfaz)</span><span class="sxs-lookup"><span data-stu-id="b32f8-102">ICorDebugValue2 Interface</span></span>
<span data-ttu-id="b32f8-103">Extiende la interfaz "ICorDebugValue" para proporcionar compatibilidad para objetos de "ICorDebugType".</span><span class="sxs-lookup"><span data-stu-id="b32f8-103">Extends the "ICorDebugValue" interface to provide support for "ICorDebugType" objects.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="b32f8-104">Métodos</span><span class="sxs-lookup"><span data-stu-id="b32f8-104">Methods</span></span>  
  
|<span data-ttu-id="b32f8-105">Método</span><span class="sxs-lookup"><span data-stu-id="b32f8-105">Method</span></span>|<span data-ttu-id="b32f8-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="b32f8-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="b32f8-107">GetExactType (método)</span><span class="sxs-lookup"><span data-stu-id="b32f8-107">GetExactType Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugvalue2-getexacttype-method.md)|<span data-ttu-id="b32f8-108">Obtiene un puntero de interfaz a una `ICorDebugType` objeto que representa el <xref:System.Type> de este valor.</span><span class="sxs-lookup"><span data-stu-id="b32f8-108">Gets an interface pointer to an `ICorDebugType` object that represents the <xref:System.Type> of this value.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b32f8-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="b32f8-109">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b32f8-110">Esta interfaz no admite que se la llame de forma remota, ya sea entre procesos o entre equipos.</span><span class="sxs-lookup"><span data-stu-id="b32f8-110">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b32f8-111">Requisitos</span><span class="sxs-lookup"><span data-stu-id="b32f8-111">Requirements</span></span>  
 <span data-ttu-id="b32f8-112">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b32f8-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b32f8-113">**Encabezado:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b32f8-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b32f8-114">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b32f8-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b32f8-115">**Versiones de .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b32f8-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b32f8-116">Vea también</span><span class="sxs-lookup"><span data-stu-id="b32f8-116">See Also</span></span>  
 [<span data-ttu-id="b32f8-117">Interfaces de depuración</span><span class="sxs-lookup"><span data-stu-id="b32f8-117">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
    
 [<span data-ttu-id="b32f8-118">ICorDebugValue3 (interfaz)</span><span class="sxs-lookup"><span data-stu-id="b32f8-118">ICorDebugValue3 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugvalue3-interface.md)