---
title: 117 - WorkflowInstanceTerminatedRecordWithId
ms.date: 03/30/2017
ms.assetid: e68539d0-5338-468a-9f75-7e5b09d39a3c
ms.openlocfilehash: d1d6930a08eeb513dbb017b6c9b409916e5b1a2c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33512403"
---
# <a name="117---workflowinstanceterminatedrecordwithid"></a>117 - WorkflowInstanceTerminatedRecordWithId
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|Id.|117|  
|Palabras clave|HealthMonitoring, WFTracking|  
|Nivel|Error|  
|Canal|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>Descripción  
 El participante de seguimiento de ETW emite este evento cuando una instancia de flujo de trabajo emite   una clase WorkflowInstanceTerminatedRecord.  
  
## <a name="message"></a>Mensaje  
 TrackRecord = WorkflowInstanceTerminatedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razón = %5, anotaciones = %6, ProfileName = %7, WorkflowDefinitionIdentity = %8  
  
## <a name="details"></a>Detalles  
  
|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|El id. de instancia del flujo de trabajo.|  
|RecordNumber|xs:long|El número de secuencia del registro emitido.|  
|EventTime|xs:dateTime|La hora en UTC cuando se emitió el evento.|  
|ActivityDefinitionId|xs:string|El nombre de la actividad raíz del flujo de trabajo.|  
|Estado|xs:string|El estado actual del flujo de trabajo.|  
|Anotaciones|xs:string|Las anotaciones que se agregaron a este evento. Los valores se almacenan en un elemento xml con el formato \<elementos >\< nombre de elemento = "annotationName" Type = "> annotationValue\</artículo > \< /artículos >. Si se especifica ninguna anotación, a continuación, la cadena contiene \<elementos / >. El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW. Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de anotación con \<elementos >...  \< /artículos >.|  
|ProfileName|xs:string|El nombre o el perfil de seguimiento que dio como resultado que se emitiera este evento.|  
|WorkflowDefinitionIdentity|xs:string|Id. de definición de flujo de trabajo.|  
|AppDomain|xs:string|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|
