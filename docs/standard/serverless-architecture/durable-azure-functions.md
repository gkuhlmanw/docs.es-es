---
title: 'Durable functions de Azure: aplicaciones sin servidor'
description: Las funciones de Azure duraderas amplían el tiempo de ejecución de Azure Functions para habilitar los flujos de trabajo con estado en el código.
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: 03197ad57813b8132fe592f4e555c6a35edbd9bd
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "49370196"
---
# <a name="durable-azure-functions"></a><span data-ttu-id="b5188-103">Durable functions de Azure</span><span class="sxs-lookup"><span data-stu-id="b5188-103">Durable Azure functions</span></span>

<span data-ttu-id="b5188-104">Al crear aplicaciones sin servidor con Azure Functions, las operaciones normalmente se ha diseñado para ejecutarse de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="b5188-104">When creating serverless applications with Azure Functions, your operations will typically be designed to run in a stateless manner.</span></span> <span data-ttu-id="b5188-105">La razón de esta opción de diseño es que como las escalas de la plataforma, resulta difícil saber qué se está ejecutando el código en los servidores.</span><span class="sxs-lookup"><span data-stu-id="b5188-105">The reason for this design choice is because as the platform scales, it becomes difficult to know what servers the code is running on.</span></span> <span data-ttu-id="b5188-106">También resulta difícil saber cuántas instancias están activas en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="b5188-106">It also becomes difficult to know how many instances are active at any given point.</span></span> <span data-ttu-id="b5188-107">Sin embargo, hay clases de aplicaciones que requieren el estado actual de un proceso que se conoce.</span><span class="sxs-lookup"><span data-stu-id="b5188-107">However, there are classes of applications that require the current state of a process to be known.</span></span> <span data-ttu-id="b5188-108">Tenga en cuenta el proceso de enviar un pedido a una tienda en línea.</span><span class="sxs-lookup"><span data-stu-id="b5188-108">Consider the process of submitting an order to an online store.</span></span> <span data-ttu-id="b5188-109">La operación de desprotección podría ser un flujo de trabajo que se compone de varias operaciones que debe conocer el estado del proceso.</span><span class="sxs-lookup"><span data-stu-id="b5188-109">The checkout operation might be a workflow that is composed of multiple operations that need to know the state of the process.</span></span> <span data-ttu-id="b5188-110">Dicha información puede incluir el inventario de productos, si el cliente tiene los créditos de su cuenta, además de los resultados del procesamiento de la tarjeta de crédito.</span><span class="sxs-lookup"><span data-stu-id="b5188-110">Such information may include the product inventory, if the customer has any credits on their account, and also the results of processing the credit card.</span></span> <span data-ttu-id="b5188-111">Estas operaciones podrían ser fácilmente sus propios flujos de trabajo internos o incluso servicios de sistemas de terceros.</span><span class="sxs-lookup"><span data-stu-id="b5188-111">These operations could easily be their own internal workflows or even services from third-party systems.</span></span>

<span data-ttu-id="b5188-112">Existen diversos patrones actualmente que ayudan a con la coordinación de estado de la aplicación entre sistemas internos y externos.</span><span class="sxs-lookup"><span data-stu-id="b5188-112">Various patterns exist today that assist with the coordination of application state between internal and external systems.</span></span> <span data-ttu-id="b5188-113">Es habitual encontrar a soluciones que se basan en los sistemas centralizados de puesta en cola, los almacenes de pares clave-valor distribuidos o bases de datos compartidos para administrar dicho estado.</span><span class="sxs-lookup"><span data-stu-id="b5188-113">It's common to come across solutions that rely on centralized queuing systems, distributed key-value stores, or shared databases to manage that state.</span></span> <span data-ttu-id="b5188-114">Sin embargo, estos son los recursos adicionales que necesitan ahora se aprovisionan y administran.</span><span class="sxs-lookup"><span data-stu-id="b5188-114">However, these are all additional resources that now need to be provisioned and managed.</span></span> <span data-ttu-id="b5188-115">En un entorno sin servidor, el código podría ser complicado intentar coordinar con estos recursos manualmente.</span><span class="sxs-lookup"><span data-stu-id="b5188-115">In a serverless environment, your code could become cumbersome trying to coordinate with these resources manually.</span></span> <span data-ttu-id="b5188-116">Las funciones de Azure ofrece una alternativa para la creación de funciones con estado de Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="b5188-116">Azure Functions offers an alternative for creating stateful functions called Durable Functions.</span></span>

<span data-ttu-id="b5188-117">Durable Functions es una extensión de Azure Functions runtime que permite la definición de flujos de trabajo con estado en el código.</span><span class="sxs-lookup"><span data-stu-id="b5188-117">Durable Functions is an extension to the Azure Functions runtime that enables the definition of stateful workflows in code.</span></span> <span data-ttu-id="b5188-118">Al dividir los flujos de trabajo en las actividades, la extensión Durable Functions puede administrar el estado, crear puntos de control de progreso y controlar la distribución de llamadas de función entre servidores.</span><span class="sxs-lookup"><span data-stu-id="b5188-118">By breaking down workflows into activities, the Durable Functions extension can manage state, create progress checkpoints, and handle the distribution of function calls across servers.</span></span> <span data-ttu-id="b5188-119">En segundo plano, permite usar una cuenta de Azure Storage para conservar el historial de ejecución, programar las funciones de actividad y recuperar las respuestas.</span><span class="sxs-lookup"><span data-stu-id="b5188-119">In the background, it makes use of an Azure Storage account to persist execution history, schedule activity functions and retrieve responses.</span></span> <span data-ttu-id="b5188-120">El código sin servidor nunca debe interactuar con la información guardada en esa cuenta de almacenamiento y normalmente no es algo con lo que los desarrolladores necesitan interactuar.</span><span class="sxs-lookup"><span data-stu-id="b5188-120">Your serverless code should never interact with persisted information in that storage account, and is typically not something with which developers need to interact.</span></span>

## <a name="triggering-a-stateful-workflow"></a><span data-ttu-id="b5188-121">Desencadenar un flujo de trabajo con estado</span><span class="sxs-lookup"><span data-stu-id="b5188-121">Triggering a stateful workflow</span></span>

<span data-ttu-id="b5188-122">Los flujos de trabajo con estado en Durable Functions pueden dividirse en dos componentes intrínsecos; desencadenadores de orquestación y la actividad.</span><span class="sxs-lookup"><span data-stu-id="b5188-122">Stateful workflows in Durable Functions can be broken down into two intrinsic components; orchestration and activity triggers.</span></span> <span data-ttu-id="b5188-123">Desencadenadores y enlaces son los componentes principales utilizados por las funciones de Azure para habilitar las funciones sin servidor para recibir una notificación cuando se inicie, recibir de entrada y da como resultado la devolución.</span><span class="sxs-lookup"><span data-stu-id="b5188-123">Triggers and bindings are core components used by Azure Functions to enable your serverless functions to be notified when to start, receive input, and return results.</span></span>

### <a name="working-with-the-orchestration-client"></a><span data-ttu-id="b5188-124">Trabajar con el cliente de orquestación</span><span class="sxs-lookup"><span data-stu-id="b5188-124">Working with the Orchestration client</span></span>

<span data-ttu-id="b5188-125">Las orquestaciones son únicas en comparación con otros estilos de las operaciones desencadenadas en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b5188-125">Orchestrations are unique when compared to other styles of triggered operations in Azure Functions.</span></span> <span data-ttu-id="b5188-126">Durable Functions permite la ejecución de funciones que pueden requerir horas o incluso días en completarse.</span><span class="sxs-lookup"><span data-stu-id="b5188-126">Durable Functions enables the execution of functions that may take hours or even days to complete.</span></span> <span data-ttu-id="b5188-127">Ese tipo de comportamiento viene de forma preventiva terminar con la necesidad de realizar la comprobación del estado de una orquestación en ejecución, o enviar notificaciones de eventos externos.</span><span class="sxs-lookup"><span data-stu-id="b5188-127">That type of behavior comes with the need to able to check the status of a running orchestration, preemptively terminate, or send notifications of external events.</span></span>

<span data-ttu-id="b5188-128">En tales casos, la extensión Durable Functions proporciona el `DurableOrchestrationClient` organizados de clase que le permite interactuar con las funciones.</span><span class="sxs-lookup"><span data-stu-id="b5188-128">For such cases, the Durable Functions extension provides the `DurableOrchestrationClient` class that allows you to interact with orchestrated functions.</span></span> <span data-ttu-id="b5188-129">Obtener acceso al cliente de orquestación mediante el `OrchestrationClientAttribute` enlace.</span><span class="sxs-lookup"><span data-stu-id="b5188-129">You get access to the orchestration client by using the `OrchestrationClientAttribute` binding.</span></span> <span data-ttu-id="b5188-130">Por lo general, debe incluir este atributo con otro tipo de desencadenador, como un `HttpTrigger` o `ServiceBusTrigger`.</span><span class="sxs-lookup"><span data-stu-id="b5188-130">Generally, you would include this attribute with another trigger type, such as an `HttpTrigger` or `ServiceBusTrigger`.</span></span> <span data-ttu-id="b5188-131">Una vez que se desencadenó la función de origen, el cliente de orquestación se puede usar para iniciar una función de orquestador.</span><span class="sxs-lookup"><span data-stu-id="b5188-131">Once the source function has been triggered, the orchestration client can be used to start an orchestrator function.</span></span>

```csharp
[FunctionName("KickOff")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient<orchestrationClient>)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

### <a name="the-orchestrator-function"></a><span data-ttu-id="b5188-132">La función de orquestador</span><span class="sxs-lookup"><span data-stu-id="b5188-132">The orchestrator function</span></span>

<span data-ttu-id="b5188-133">Anotar una función con el OrchestrationTriggerAttribute en marcas de Azure Functions que funcionan como una función de orquestador.</span><span class="sxs-lookup"><span data-stu-id="b5188-133">Annotating a function with the OrchestrationTriggerAttribute in Azure Functions marks that function as an orchestrator function.</span></span> <span data-ttu-id="b5188-134">Es responsable de administrar las diversas actividades que constituyen el flujo de trabajo con estado.</span><span class="sxs-lookup"><span data-stu-id="b5188-134">It's responsible for managing the various activities that make up your stateful workflow.</span></span>

<span data-ttu-id="b5188-135">Las funciones de orquestador son no se puede hacer uso de enlaces que no sea el OrchestrationTriggerAttribute.</span><span class="sxs-lookup"><span data-stu-id="b5188-135">Orchestrator functions are unable to make use of bindings other than the OrchestrationTriggerAttribute.</span></span> <span data-ttu-id="b5188-136">Este atributo solo puede usarse con un tipo de parámetro de DurableOrchestrationContext.</span><span class="sxs-lookup"><span data-stu-id="b5188-136">This attribute can only be used with a parameter type of DurableOrchestrationContext.</span></span> <span data-ttu-id="b5188-137">Puesto que no se admite la deserialización de entradas en la firma de función, no se pueden usar ningún otras entradas.</span><span class="sxs-lookup"><span data-stu-id="b5188-137">No other inputs can be used since deserialization of inputs in the function signature isn't supported.</span></span> <span data-ttu-id="b5188-138">Para obtener las entradas proporcionadas por el cliente de orquestación, el GetInput\<T\> se debe usar el método.</span><span class="sxs-lookup"><span data-stu-id="b5188-138">To get inputs provided by the orchestration client, the GetInput\<T\> method must be used.</span></span>

<span data-ttu-id="b5188-139">Además, los tipos devueltos de las funciones de orquestación deben ser void, Task o un valor serializable de JSON.</span><span class="sxs-lookup"><span data-stu-id="b5188-139">Also, the return types of orchestration functions must be either void, Task, or a JSON serializable value.</span></span>

> <span data-ttu-id="b5188-140">*Código de control de errores se ha omitido por razones de brevedad*</span><span class="sxs-lookup"><span data-stu-id="b5188-140">*Error handling code has been left out for brevity*</span></span>

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<string>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

<span data-ttu-id="b5188-141">Varias instancias de una orquestación pueden ser iniciado y en ejecución al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5188-141">Multiple instances of an orchestration can be started and running at the same time.</span></span> <span data-ttu-id="b5188-142">Una llamada a la `StartNewAsync` método en el `DurableOrchestrationClient` inicia una nueva instancia de la orquestación.</span><span class="sxs-lookup"><span data-stu-id="b5188-142">Calling the `StartNewAsync` method on the `DurableOrchestrationClient` launches a new instance of the orchestration.</span></span> <span data-ttu-id="b5188-143">El método devuelve un `Task<string>` que se completa cuando se inició la orquestación.</span><span class="sxs-lookup"><span data-stu-id="b5188-143">The method returns a `Task<string>` that completes when the orchestration has started.</span></span> <span data-ttu-id="b5188-144">Una excepción de tipo `TimeoutException` cuando se genera si no se ha iniciado la orquestación en 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="b5188-144">An exception of type `TimeoutException` gets thrown if the orchestration hasn't started within 30 seconds.</span></span>

<span data-ttu-id="b5188-145">Completado `Task<string>` desde `StartNewAsync` debe contener el identificador único de la instancia de orquestación.</span><span class="sxs-lookup"><span data-stu-id="b5188-145">The completed `Task<string>` from `StartNewAsync` should contain the unique ID of the orchestration instance.</span></span> <span data-ttu-id="b5188-146">Este Id. de instancia puede usarse para invocar operaciones en esa orquestación específica.</span><span class="sxs-lookup"><span data-stu-id="b5188-146">This instance ID can be used to invoke operations on that specific orchestration.</span></span> <span data-ttu-id="b5188-147">La orquestación se puede consultar el estado o envía notificaciones de eventos.</span><span class="sxs-lookup"><span data-stu-id="b5188-147">The orchestration can be queried for the status or sent event notifications.</span></span>

### <a name="the-activity-functions"></a><span data-ttu-id="b5188-148">Las funciones de actividad</span><span class="sxs-lookup"><span data-stu-id="b5188-148">The activity functions</span></span>

<span data-ttu-id="b5188-149">Las funciones de actividad son las operaciones discretas que obtengan compondrán juntos dentro de una función de orquestación para crear el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5188-149">Activity functions are the discrete operations that get composed together within an orchestration function to create the workflow.</span></span> <span data-ttu-id="b5188-150">Aquí es donde la mayoría del trabajo real tendrá lugar.</span><span class="sxs-lookup"><span data-stu-id="b5188-150">Here is where most of actual work would take place.</span></span> <span data-ttu-id="b5188-151">Representan la lógica de negocios, largos procesos en ejecución y las piezas del rompecabezas para una solución mayor.</span><span class="sxs-lookup"><span data-stu-id="b5188-151">They represent the business logic, long running processes, and the puzzle pieces to a larger solution.</span></span>

<span data-ttu-id="b5188-152">El `ActivityTriggerAttribute` se usa para anotar un parámetro de función de tipo `DurableActivityContext`.</span><span class="sxs-lookup"><span data-stu-id="b5188-152">The `ActivityTriggerAttribute` is used to annotate a function parameter of type `DurableActivityContext`.</span></span> <span data-ttu-id="b5188-153">Mediante la anotación indica el tiempo de ejecución que la función está pensada para usarse como una función de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5188-153">Using the annotation informs the runtime that the function is intended to be used as an activity function.</span></span> <span data-ttu-id="b5188-154">Se recuperan valores de entrada a las funciones de actividad mediante la `GetInput<T>` método de la `DurableActivityContext` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b5188-154">Input values to activity functions are retrieved using the `GetInput<T>` method of the `DurableActivityContext` parameter.</span></span>

<span data-ttu-id="b5188-155">Al igual que las funciones de orquestación, los tipos devueltos de funciones de actividad deben ser void, Task o un valor serializable de JSON.</span><span class="sxs-lookup"><span data-stu-id="b5188-155">Similar to orchestration functions, the return types of activity functions must be either void, Task, or a JSON serializable value.</span></span>

<span data-ttu-id="b5188-156">Las excepciones no controladas que se producen dentro de las funciones de actividad obtendrá enviadas a la función de orquestador que realiza la llamada y se presenta como un `TaskFailedException`.</span><span class="sxs-lookup"><span data-stu-id="b5188-156">Any unhandled exceptions that get thrown within activity functions will get sent up to the calling orchestrator function and presented as a `TaskFailedException`.</span></span> <span data-ttu-id="b5188-157">En este momento, el error se puede detectar y registrar en el orquestador, y se puede reintentar la actividad.</span><span class="sxs-lookup"><span data-stu-id="b5188-157">At this point, the error can be caught and logged in the orchestrator, and the activity can be retried.</span></span>

```csharp
[FunctionName("CheckAndReserveInventory")]
public static bool CheckAndReserveInventory([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    // Connect to inventory system and try to reserve items
    return true;
}
```

## <a name="recommended-resources"></a><span data-ttu-id="b5188-158">Recursos recomendados</span><span class="sxs-lookup"><span data-stu-id="b5188-158">Recommended resources</span></span>

* [<span data-ttu-id="b5188-159">Durable Functions</span><span class="sxs-lookup"><span data-stu-id="b5188-159">Durable Functions</span></span>](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)
* [<span data-ttu-id="b5188-160">Enlaces para Durable Functions</span><span class="sxs-lookup"><span data-stu-id="b5188-160">Bindings for Durable Functions</span></span>](https://docs.microsoft.com/azure/azure-functions/durable-functions-bindings)
* [<span data-ttu-id="b5188-161">Administración de instancias con Durable Functions</span><span class="sxs-lookup"><span data-stu-id="b5188-161">Manage instances in Durable Functions</span></span>](https://docs.microsoft.com/azure/azure-functions/durable-functions-instance-management)

>[!div class="step-by-step"]
<span data-ttu-id="b5188-162">[Anterior](event-grid.md)
[Siguiente](orchestration-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="b5188-162">[Previous](event-grid.md)
[Next](orchestration-patterns.md)</span></span>