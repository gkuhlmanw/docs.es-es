---
title: Modificador del parámetro in (referencia de C#)
ms.date: 03/06/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 3c15cc0dce5b37866fd826e3d6b9adcb00724672
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="in-parameter-modifier-c-reference"></a><span data-ttu-id="3d95e-102">Modificador del parámetro in (referencia de C#)</span><span class="sxs-lookup"><span data-stu-id="3d95e-102">in parameter modifier (C# Reference)</span></span>

<span data-ttu-id="3d95e-103">La palabra clave `in` hace que los argumentos se pasen por referencia.</span><span class="sxs-lookup"><span data-stu-id="3d95e-103">The `in` keyword causes arguments to be passed by reference.</span></span> <span data-ttu-id="3d95e-104">Es como las palabras clave [ref](ref.md) o [out](out-parameter-modifier.md), salvo que el método llamado no puede modificar los argumentos `in`. Mientras que los argumentos `ref` sí se pueden modificar, los argumentos `out` debe modificarlos el llamador, y estas modificaciones se pueden observar en el contexto de llamada.</span><span class="sxs-lookup"><span data-stu-id="3d95e-104">It is like the [ref](ref.md) or [out](out-parameter-modifier.md) keywords, except that `in` arguments cannot be modified by the called method, whereas `ref` arguments may be modified,  `out` arguments must be modified by the caller, and those modifications are observable in the calling context.</span></span>

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

<span data-ttu-id="3d95e-105">En el ejemplo anterior se muestra que el modificador `in` no suele ser necesario en el sitio de llamada,</span><span class="sxs-lookup"><span data-stu-id="3d95e-105">The preceding example demonstrates the `in` modifier is usually unnecessary at the call site.</span></span> <span data-ttu-id="3d95e-106">sino que solo lo es en la declaración del método.</span><span class="sxs-lookup"><span data-stu-id="3d95e-106">It is only required in the method declaration.</span></span>

> [!NOTE] 
> <span data-ttu-id="3d95e-107">Además, la palabra clave `in` puede usarse con un parámetro de tipo genérico para especificar que el parámetro de tipo es contravariante, parte de una instrucción `foreach` o de una cláusula `join` de una consulta de LINQ.</span><span class="sxs-lookup"><span data-stu-id="3d95e-107">The `in` keyword can also be used with a generic type parameter to specify that the type parameter is contravariant, as part of a `foreach` statement, or as part of a `join` clause in a LINQ query.</span></span> <span data-ttu-id="3d95e-108">Para más información sobre el uso de la palabra clave `in` en esos contextos, vea [in](in.md), que además incluye vínculos a todos estos usos.</span><span class="sxs-lookup"><span data-stu-id="3d95e-108">For more information on the use of the `in` keyword in these contexts, see [in](in.md), which provides links to all those uses.</span></span>
  
 <span data-ttu-id="3d95e-109">Las variables que se han pasado como argumentos `in` deben inicializarse antes de pasarse en una llamada de método.</span><span class="sxs-lookup"><span data-stu-id="3d95e-109">Variables passed as `in` arguments must be initialized before being passed in a method call.</span></span> <span data-ttu-id="3d95e-110">Sin embargo, es posible que el método llamado no asigne ningún valor o modifique el argumento.</span><span class="sxs-lookup"><span data-stu-id="3d95e-110">However, the called method may not assign a value or modify the argument.</span></span>  
  
 <span data-ttu-id="3d95e-111">Aunque las palabras clave `in`, `ref` y `out` causan un comportamiento diferente en tiempo de ejecución, no se consideran parte de la signatura del método en tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="3d95e-111">Although the `in`, `ref`, and `out` keywords cause different run-time behavior, they are not considered part of the method signature at compile time.</span></span> <span data-ttu-id="3d95e-112">Por lo tanto, los métodos no pueden sobrecargarse si la única diferencia es que un método toma un argumento `ref` o `in` y el otro toma un argumento `out`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-112">Therefore, methods cannot be overloaded if the only difference is that one method takes a `ref` or `in` argument and the other takes an `out` argument.</span></span> <span data-ttu-id="3d95e-113">Por ejemplo, el código siguiente, no se compilará:</span><span class="sxs-lookup"><span data-stu-id="3d95e-113">The following code, for example, will not compile:</span></span>  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
<span data-ttu-id="3d95e-114">Está permitida la sobrecarga en función de la presencia de `in`:</span><span class="sxs-lookup"><span data-stu-id="3d95e-114">Overloading based on the presence of `in` is allowed:</span></span>  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a><span data-ttu-id="3d95e-115">Reglas de resolución de sobrecarga</span><span class="sxs-lookup"><span data-stu-id="3d95e-115">Overload resolution rules</span></span>

<span data-ttu-id="3d95e-116">Puede comprender las reglas de resolución de sobrecarga de métodos por valor frente a argumentos `in` mediante la comprensión de la motivación de argumentos `in`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-116">You can understand the overload resolution rules for methods with by value vs. `in` arguments through understanding the motivation for `in` arguments.</span></span> <span data-ttu-id="3d95e-117">Definir métodos usando parámetros `in` es una optimización del rendimiento potencial.</span><span class="sxs-lookup"><span data-stu-id="3d95e-117">Defining methods using `in` parameters is a potential performance optimization.</span></span> <span data-ttu-id="3d95e-118">Algunos argumentos de tipo `struct` pueden tener un gran tamaño y, cuando se llama a métodos en bucles de pequeñas dimensiones o rutas de acceso de código crítico, el costo de copiar esas estructuras resulta crucial.</span><span class="sxs-lookup"><span data-stu-id="3d95e-118">Some `struct` type arguments may be large in size, and when methods are called in tight loops or critical code paths, the cost of copying those structures is critical.</span></span> <span data-ttu-id="3d95e-119">Los métodos declaran parámetros `in` para especificar qué argumentos pueden pasarse por referencia sin ningún riesgo porque el método llamado no modifica el estado de ese argumento.</span><span class="sxs-lookup"><span data-stu-id="3d95e-119">Methods declare `in` parameters to specify that arguments may be passed by reference safely because the called method does not modify the state of that argument.</span></span> <span data-ttu-id="3d95e-120">Al pasar esos argumentos por referencia se evita la copia (potencialmente) costosa.</span><span class="sxs-lookup"><span data-stu-id="3d95e-120">Passing those arguments by reference avoids the (potentially) expensive copy.</span></span> 

<span data-ttu-id="3d95e-121">Especificar `in` en argumentos en el sitio de llamada suele ser opcional.</span><span class="sxs-lookup"><span data-stu-id="3d95e-121">Specifying `in` on arguments at the call site is typically optional.</span></span> <span data-ttu-id="3d95e-122">No hay ninguna diferencia semántica entre pasar argumentos por valor y pasarlos por referencia mediante el modificador `in`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-122">There is no semantic difference between passing arguments by value and passing them by reference using the `in` modifier.</span></span> <span data-ttu-id="3d95e-123">El modificador `in` en el sitio de llamada es opcional porque no es necesario indicar que podría cambiarse el valor del argumento.</span><span class="sxs-lookup"><span data-stu-id="3d95e-123">The `in` modifier at the call site is optional because you don't need to indicate that the argument's value might be changed.</span></span> <span data-ttu-id="3d95e-124">Se agrega explícitamente el modificador `in` en el sitio de llamada para garantizar que el argumento se pasa por referencia, y no por valor.</span><span class="sxs-lookup"><span data-stu-id="3d95e-124">You explicitly add the `in` modifier at the call site to ensure the argument is passed by reference, not by value.</span></span> <span data-ttu-id="3d95e-125">Usar explícitamente `in` tiene dos efectos:</span><span class="sxs-lookup"><span data-stu-id="3d95e-125">Explicitly using `in` has two effects:</span></span>

<span data-ttu-id="3d95e-126">El primero es que, al especificar `in` en el sitio de llamada, se fuerza al compilador a seleccionar un método definido con un parámetro `in` coincidente.</span><span class="sxs-lookup"><span data-stu-id="3d95e-126">First, specifying `in` at the call site forces the compiler to select a method defined with a matching `in` parameter.</span></span> <span data-ttu-id="3d95e-127">En caso contrario, cuando dos métodos se diferencian solo en presencia de `in`, la sobrecarga por valor es una coincidencia mejor.</span><span class="sxs-lookup"><span data-stu-id="3d95e-127">Otherwise, when two methods differ only in the presence of `in`, the by value overload is a better match.</span></span>

<span data-ttu-id="3d95e-128">El segundo es que, al especificar `in` declara su intención para pasar un argumento por referencia.</span><span class="sxs-lookup"><span data-stu-id="3d95e-128">Second, specifying `in` declares your intent to pass an argument by reference.</span></span> <span data-ttu-id="3d95e-129">Los argumentos usados con `in` deben representar una ubicación a la que se pueda hacer referencia directamente.</span><span class="sxs-lookup"><span data-stu-id="3d95e-129">The argument used with `in` must represent a location that can be directly referred to.</span></span> <span data-ttu-id="3d95e-130">Se aplican las mismas reglas generales para los argumentos `out` y `ref`: no se pueden usar constantes, propiedades normales u otras expresiones que produzcan valores.</span><span class="sxs-lookup"><span data-stu-id="3d95e-130">The same general rules for `out` and `ref` arguments apply: You cannot use constants, ordinary properties, or other expressions that produce values.</span></span> <span data-ttu-id="3d95e-131">En caso contrario, si se omite `in` en el sitio de llamada, se informa al compilador de que le permitirá crear una variable temporal para pasar por referencia de solo lectura para el método.</span><span class="sxs-lookup"><span data-stu-id="3d95e-131">Otherwise, omitting `in` at the call site informs the compiler that you will allow it to create a temporary variable to pass by read-only reference to the method.</span></span> <span data-ttu-id="3d95e-132">El compilador crea una variable temporal para superar varias restricciones con argumentos `in`:</span><span class="sxs-lookup"><span data-stu-id="3d95e-132">The compiler creates a temporary variable to overcome several restrictions with `in` arguments:</span></span>

- <span data-ttu-id="3d95e-133">Una variable temporal permite constantes en tiempo de compilación como parámetros `in`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-133">A temporary variable allows compile-time constants as `in` parameters.</span></span>
- <span data-ttu-id="3d95e-134">Una variable temporal permite propiedades u otras expresiones para parámetros `in`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-134">A temporary variable allows properties, or other expressions for `in` parameters.</span></span>
- <span data-ttu-id="3d95e-135">Una variable temporal permite argumentos en los que hay una conversión implícita desde el tipo de argumento hacia el tipo de parámetro.</span><span class="sxs-lookup"><span data-stu-id="3d95e-135">A temporary variable allows arguments where there is an implicit conversion from the argument type to the parameter type.</span></span>

<span data-ttu-id="3d95e-136">En todas las instancias anteriores, el compilador crea una variable temporal que almacena el valor de la constante, la propiedad u otra expresión.</span><span class="sxs-lookup"><span data-stu-id="3d95e-136">In all the preceding instances, the compiler creates a temporary variable that stores the value of the constant, property, or other expression.</span></span>

<span data-ttu-id="3d95e-137">Estas reglas se muestran en este código:</span><span class="sxs-lookup"><span data-stu-id="3d95e-137">The following code illustrates these rules:</span></span>

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

<span data-ttu-id="3d95e-138">Supongamos ahora que hay disponible otro método que usa argumentos por valor.</span><span class="sxs-lookup"><span data-stu-id="3d95e-138">Now, suppose another method using by value arguments was available.</span></span> <span data-ttu-id="3d95e-139">Los resultados cambian como se muestra en este código:</span><span class="sxs-lookup"><span data-stu-id="3d95e-139">The results change as shown in the following code:</span></span>

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

<span data-ttu-id="3d95e-140">La única llamada de método donde se pasa el argumento por referencia es la última.</span><span class="sxs-lookup"><span data-stu-id="3d95e-140">The only method call where the argument is passed by reference is the final one.</span></span>

> [!NOTE]
> <span data-ttu-id="3d95e-141">El código anterior usa `int` como el tipo de argumento para simplificar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="3d95e-141">The preceding code uses `int` as the argument type for simplicity.</span></span> <span data-ttu-id="3d95e-142">Como `int` no es más grande que una referencia en la mayoría de máquinas modernas, no supone ninguna ventaja pasar un único `int` como una referencia de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="3d95e-142">Because `int` is no larger than a reference in most modern machines, there is no benefit to passing a single `int` as a readonly reference.</span></span> 

## <a name="limitations-on-in-parameters"></a><span data-ttu-id="3d95e-143">Limitaciones de los parámetros `in`</span><span class="sxs-lookup"><span data-stu-id="3d95e-143">Limitations on `in` parameters</span></span>

<span data-ttu-id="3d95e-144">Las palabras clave `in`, `ref` y `out` no pueden usarse para estos tipos de métodos:</span><span class="sxs-lookup"><span data-stu-id="3d95e-144">You can't use the `in`, `ref`, and `out` keywords for the following kinds of methods:</span></span>  
  
- <span data-ttu-id="3d95e-145">Métodos asincrónicos, que se definen mediante el uso del modificador [async](async.md).</span><span class="sxs-lookup"><span data-stu-id="3d95e-145">Async methods, which you define by using the [async](async.md) modifier.</span></span>  
- <span data-ttu-id="3d95e-146">Métodos de iterador, que incluyen una instrucción [yield return](yield.md) o `yield break`.</span><span class="sxs-lookup"><span data-stu-id="3d95e-146">Iterator methods, which include a [yield return](yield.md) or `yield break` statement.</span></span>  

## <a name="c-language-specification"></a><span data-ttu-id="3d95e-147">Especificación del lenguaje C#</span><span class="sxs-lookup"><span data-stu-id="3d95e-147">C# Language Specification</span></span>  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a><span data-ttu-id="3d95e-148">Vea también</span><span class="sxs-lookup"><span data-stu-id="3d95e-148">See Also</span></span>  
 [<span data-ttu-id="3d95e-149">Referencia de C#</span><span class="sxs-lookup"><span data-stu-id="3d95e-149">C# Reference</span></span>](../index.md)  
 [<span data-ttu-id="3d95e-150">Guía de programación de C#</span><span class="sxs-lookup"><span data-stu-id="3d95e-150">C# Programming Guide</span></span>](../../programming-guide/index.md)  
 [<span data-ttu-id="3d95e-151">Palabras clave de C#</span><span class="sxs-lookup"><span data-stu-id="3d95e-151">C# Keywords</span></span>](index.md)  
 <span data-ttu-id="3d95e-152">[Parámetros de método](method-parameters.md) [Semántica de referencia con tipos de valor](../../reference-semantics-with-value-types.md)</span><span class="sxs-lookup"><span data-stu-id="3d95e-152">[Method Parameters](method-parameters.md) [Reference Semantics with Value Types](../../reference-semantics-with-value-types.md)</span></span>