---
title: Оператор await — справочник по C#
ms.custom: seodec18
ms.date: 08/30/2019
f1_keywords:
- await_CSharpKeyword
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
ms.openlocfilehash: c2172f651dd106825680de3195e26f032225a9ab
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169332"
---
# <a name="await-operator-c-reference"></a><span data-ttu-id="51bf7-102">Оператор await (справочник по C#)</span><span class="sxs-lookup"><span data-stu-id="51bf7-102">await operator (C# reference)</span></span>

<span data-ttu-id="51bf7-103">Оператор `await` приостанавливает вычисление включающего [асинхронного](../keywords/async.md) метода до завершения асинхронной операции, представленной его операндом.</span><span class="sxs-lookup"><span data-stu-id="51bf7-103">The `await` operator suspends evaluation of the enclosing [async](../keywords/async.md) method until the asynchronous operation represented by its operand completes.</span></span> <span data-ttu-id="51bf7-104">После завершения асинхронной операции оператор `await` возвращает результат операции, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="51bf7-104">When the asynchronous operation completes, the `await` operator returns the result of the operation, if any.</span></span> <span data-ttu-id="51bf7-105">Когда оператор `await` применяется к операнду, который представляет уже завершенную операцию, он возвращает результат операции немедленно без приостановки включающего метода.</span><span class="sxs-lookup"><span data-stu-id="51bf7-105">When the `await` operator is applied to the operand that represents already completed operation, it returns the result of the operation immediately without suspension of the enclosing method.</span></span> <span data-ttu-id="51bf7-106">Оператор `await` не блокирует поток, который вычисляет асинхронный метод.</span><span class="sxs-lookup"><span data-stu-id="51bf7-106">The `await` operator doesn't block the thread that evaluates the async method.</span></span> <span data-ttu-id="51bf7-107">Когда оператор `await` приостанавливает включающий метод, элемент управления возвращается вызывающему объекту метода.</span><span class="sxs-lookup"><span data-stu-id="51bf7-107">When the `await` operator suspends the enclosing method, the control returns to the caller of the method.</span></span>

<span data-ttu-id="51bf7-108">В следующем примере метод <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=nameWithType> возвращает экземпляр `Task<byte[]>`, который представляет асинхронную операцию, создающую массив байтов после завершения.</span><span class="sxs-lookup"><span data-stu-id="51bf7-108">In the following example, the <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=nameWithType> method returns the `Task<byte[]>` instance, which represents an asynchronous operation that produces a byte array when it completes.</span></span> <span data-ttu-id="51bf7-109">До завершения операции оператор `await` приостанавливает метод `DownloadDocsMainPageAsync`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-109">Until the operation completes, the `await` operator suspends the `DownloadDocsMainPageAsync` method.</span></span> <span data-ttu-id="51bf7-110">Когда `DownloadDocsMainPageAsync` приостанавливается, управление возвращается методу `Main`, который является вызывающим объектом `DownloadDocsMainPageAsync`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-110">When `DownloadDocsMainPageAsync` gets suspended, control is returned to the `Main` method, which is the caller of `DownloadDocsMainPageAsync`.</span></span> <span data-ttu-id="51bf7-111">Метод `Main` выполняется до тех пор, пока ему не потребуется результат асинхронной операции, выполняемой методом `DownloadDocsMainPageAsync`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-111">The `Main` method executes until it needs the result of the asynchronous operation performed by the `DownloadDocsMainPageAsync` method.</span></span> <span data-ttu-id="51bf7-112">Когда <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> получает все байты, вычисляется остальная часть метода `DownloadDocsMainPageAsync`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-112">When <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> gets all the bytes, the rest of the `DownloadDocsMainPageAsync` method is evaluated.</span></span> <span data-ttu-id="51bf7-113">После этого вычисляется остальная часть метода `Main`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-113">After that, the rest of the `Main` method is evaluated.</span></span>

[!code-csharp[await example](~/samples/csharp/language-reference/operators/AwaitOperator.cs)]

<span data-ttu-id="51bf7-114">В предыдущем примере используется [асинхронный метод `Main`](../../programming-guide/main-and-command-args/index.md), который доступен начиная с версии C# 7.1.</span><span class="sxs-lookup"><span data-stu-id="51bf7-114">The preceding example uses the [async `Main` method](../../programming-guide/main-and-command-args/index.md), which is possible starting with C# 7.1.</span></span> <span data-ttu-id="51bf7-115">Дополнительные сведения см. в описании [оператора await в методе Main](#await-operator-in-the-main-method).</span><span class="sxs-lookup"><span data-stu-id="51bf7-115">For more information, see the [await operator in the Main method](#await-operator-in-the-main-method) section.</span></span>

> [!NOTE]
> <span data-ttu-id="51bf7-116">Общие сведения об асинхронном программировании см. в разделе [Асинхронное программирование с использованием ключевых слов async и await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-116">For an introduction to asynchronous programming, see [Asynchronous programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="51bf7-117">Асинхронное программирование `async` и `await` следует [асинхронной модели, основанной на задачах](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-117">Asynchronous programming with `async` and `await` follows the [task-based asynchronous pattern](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).</span></span>

<span data-ttu-id="51bf7-118">Оператор `await` можно использовать только в методе, [лямбда-выражении](../../programming-guide/statements-expressions-operators/lambda-expressions.md) или в [анонимном методе](delegate-operator.md), изменяемом ключевым словом [async](../keywords/async.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-118">You can use the `await` operator only in a method, [lambda expression](../../programming-guide/statements-expressions-operators/lambda-expressions.md), or [anonymous method](delegate-operator.md) that is modified by the [async](../keywords/async.md) keyword.</span></span> <span data-ttu-id="51bf7-119">В асинхронном методе нельзя использовать оператор `await` в теле синхронной функции, внутри блока [инструкции lock](../keywords/lock-statement.md) и в [ненадежном](../keywords/unsafe.md) контексте.</span><span class="sxs-lookup"><span data-stu-id="51bf7-119">Within an async method, you cannot use the `await` operator in the body of a synchronous function, inside the block of a [lock statement](../keywords/lock-statement.md), and in an [unsafe](../keywords/unsafe.md) context.</span></span>
  
<span data-ttu-id="51bf7-120">Операнд оператора `await` обычно имеет один из следующих типов .NET: <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask> или <xref:System.Threading.Tasks.ValueTask%601>.</span><span class="sxs-lookup"><span data-stu-id="51bf7-120">The operand of the `await` operator is usually of one of the following .NET types: <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask>, or <xref:System.Threading.Tasks.ValueTask%601>.</span></span> <span data-ttu-id="51bf7-121">Однако любое ожидаемое выражение может быть операндом оператора `await`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-121">However, any awaitable expression can be the operand of the `await` operator.</span></span> <span data-ttu-id="51bf7-122">Дополнительные сведения см. в разделе об [ожидаемых выражениях](~/_csharplang/spec/expressions.md#awaitable-expressions) в [спецификации языка C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-122">For more information, see the [Awaitable expressions](~/_csharplang/spec/expressions.md#awaitable-expressions) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="51bf7-123">Тип выражения `await t` является `TResult`, если тип выражения `t` является <xref:System.Threading.Tasks.Task%601> или <xref:System.Threading.Tasks.ValueTask%601>.</span><span class="sxs-lookup"><span data-stu-id="51bf7-123">The type of expression `await t` is `TResult` if the type of expression `t` is <xref:System.Threading.Tasks.Task%601> or <xref:System.Threading.Tasks.ValueTask%601>.</span></span> <span data-ttu-id="51bf7-124">Если тип `t` является <xref:System.Threading.Tasks.Task> или <xref:System.Threading.Tasks.ValueTask>, тип `await t` является `void`.</span><span class="sxs-lookup"><span data-stu-id="51bf7-124">If the type of `t` is <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.ValueTask>, the type of `await t` is `void`.</span></span> <span data-ttu-id="51bf7-125">В обоих случаях, если `t` вызывает исключение, `await t` воспроизводит это исключение.</span><span class="sxs-lookup"><span data-stu-id="51bf7-125">In both cases, if `t` throws an exception, `await t` rethrows the exception.</span></span> <span data-ttu-id="51bf7-126">Дополнительные сведения об обработке исключений см. в разделе [Исключения в асинхронных методах](../keywords/try-catch.md#exceptions-in-async-methods) в статье о [try-catch](../keywords/try-catch.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-126">For more information about exception handling, see the [Exceptions in async methods](../keywords/try-catch.md#exceptions-in-async-methods) section of the [try-catch statement](../keywords/try-catch.md) article.</span></span>

<span data-ttu-id="51bf7-127">Ключевые слова `async` и `await` доступны начиная с C# 5.</span><span class="sxs-lookup"><span data-stu-id="51bf7-127">The `async` and `await` keywords are available starting with C# 5.</span></span>

## <a name="await-operator-in-the-main-method"></a><span data-ttu-id="51bf7-128">Оператор await в методе Main</span><span class="sxs-lookup"><span data-stu-id="51bf7-128">await operator in the Main method</span></span>

<span data-ttu-id="51bf7-129">Начиная с C# 7,1 [метод `Main`](../../programming-guide/main-and-command-args/index.md), который является точкой входа приложения, может возвращать `Task` или `Task<int>`, что позволяет использовать оператор `await` в теле.</span><span class="sxs-lookup"><span data-stu-id="51bf7-129">Starting with C# 7.1, the [`Main` method](../../programming-guide/main-and-command-args/index.md), which is the application entry point, can return `Task` or `Task<int>`, enabling it to be async so you can use the `await` operator in its body.</span></span> <span data-ttu-id="51bf7-130">В более ранних версиях C#, чтобы убедиться, что метод `Main` ожидает завершения асинхронной операции, можно получить значение свойства <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> экземпляра <xref:System.Threading.Tasks.Task%601>, возвращаемого соответствующим асинхронным методом.</span><span class="sxs-lookup"><span data-stu-id="51bf7-130">In earlier C# versions, to ensure that the `Main` method waits for the completion of an asynchronous operation, you can retrieve the value of the <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> property of the <xref:System.Threading.Tasks.Task%601> instance that is returned by the corresponding async method.</span></span> <span data-ttu-id="51bf7-131">Для асинхронных операций, которые не создают значение, можно вызвать метод <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="51bf7-131">For asynchronous operations that don't produce a value, you can call the <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="51bf7-132">Ознакомьтесь со сведениями о том, [как выбрать версию языка C#](../configure-language-version.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-132">For information about how to select the language version, see [Select the C# language version](../configure-language-version.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="51bf7-133">Спецификация языка C#</span><span class="sxs-lookup"><span data-stu-id="51bf7-133">C# language specification</span></span>

<span data-ttu-id="51bf7-134">Дополнительные сведения см. в разделе об [ожидаемых выражениях](~/_csharplang/spec/expressions.md#await-expressions) в [спецификации языка C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51bf7-134">For more information, see the [Await expressions](~/_csharplang/spec/expressions.md#await-expressions) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="51bf7-135">См. также</span><span class="sxs-lookup"><span data-stu-id="51bf7-135">See also</span></span>

- [<span data-ttu-id="51bf7-136">справочник по C#</span><span class="sxs-lookup"><span data-stu-id="51bf7-136">C# reference</span></span>](../index.md)
- [<span data-ttu-id="51bf7-137">Операторы в C#</span><span class="sxs-lookup"><span data-stu-id="51bf7-137">C# operators</span></span>](index.md)
- [<span data-ttu-id="51bf7-138">async</span><span class="sxs-lookup"><span data-stu-id="51bf7-138">async</span></span>](../keywords/async.md)
- [<span data-ttu-id="51bf7-139">Асинхронное программирование с использованием ключевых слов async и await</span><span class="sxs-lookup"><span data-stu-id="51bf7-139">Asynchronous programming with async and await</span></span>](../../programming-guide/concepts/async/index.md)
- [<span data-ttu-id="51bf7-140">Асинхронная модель программирования</span><span class="sxs-lookup"><span data-stu-id="51bf7-140">Task asynchronous programming model</span></span>](../../programming-guide/concepts/async/task-asynchronous-programming-model.md)
- [<span data-ttu-id="51bf7-141">Асинхронное программирование</span><span class="sxs-lookup"><span data-stu-id="51bf7-141">Asynchronous programming</span></span>](../../async.md)
- [<span data-ttu-id="51bf7-142">Асинхронная модель на основе задач</span><span class="sxs-lookup"><span data-stu-id="51bf7-142">Task-based asynchronous pattern</span></span>](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)
- [<span data-ttu-id="51bf7-143">Подробный обзор асинхронного программирования</span><span class="sxs-lookup"><span data-stu-id="51bf7-143">Async in depth</span></span>](../../../standard/async-in-depth.md)
- [<span data-ttu-id="51bf7-144">Пошаговое руководство. Получение доступа к Интернету с помощью async и await</span><span class="sxs-lookup"><span data-stu-id="51bf7-144">Walkthrough: accessing the Web by using async and await</span></span>](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)