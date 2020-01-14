---
title: Сравнение с System. Data. SQLite
ms.date: 12/13/2019
description: Описывает некоторые различия между библиотеками Microsoft. Data. SQLite и System. Data. SQLite.
ms.openlocfilehash: 076bbc6f746cf9296c96ec73047397a21a3b2558
ms.sourcegitcommit: 7088f87e9a7da144266135f4b2397e611cf0a228
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2020
ms.locfileid: "75900714"
---
# <a name="comparison-to-systemdatasqlite"></a><span data-ttu-id="fe29d-103">Сравнение с System. Data. SQLite</span><span class="sxs-lookup"><span data-stu-id="fe29d-103">Comparison to System.Data.SQLite</span></span>

<span data-ttu-id="fe29d-104">В 2005 Роберт Симпсон создал System. Data. SQLite, поставщик SQLite для ADO.NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="fe29d-104">In 2005, Robert Simpson created System.Data.SQLite, a SQLite provider for ADO.NET 2.0.</span></span> <span data-ttu-id="fe29d-105">В 2010 команда SQLite заняла обслуживание и разработку проекта.</span><span class="sxs-lookup"><span data-stu-id="fe29d-105">In 2010, the SQLite team took over maintenance and development of the project.</span></span> <span data-ttu-id="fe29d-106">Также стоит отметить, что команда Mono Развилка код в 2007 как Mono. Data. SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-106">It's also worth noting that the Mono team forked the code in 2007 as Mono.Data.Sqlite.</span></span> <span data-ttu-id="fe29d-107">System. Data. SQLite имеет долгий журнал и превратился в стабильный и полнофункциональный поставщик ADO.NET с помощью инструментов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe29d-107">System.Data.SQLite has a long history and has evolved into a stable and full-featured ADO.NET provider complete with Visual Studio tooling.</span></span> <span data-ttu-id="fe29d-108">Новые выпуски продолжат поставлять сборки, совместимые с каждой версией .NET Framework обратно в версии 2,0 и даже .NET Compact Framework 3,5.</span><span class="sxs-lookup"><span data-stu-id="fe29d-108">New releases continue to ship assemblies compatible with every version of .NET Framework back to version 2.0 and even .NET Compact Framework 3.5.</span></span>

<span data-ttu-id="fe29d-109">Первая версия .NET Core (выпущенная в 2016) была единственной, простой, современной и кросс-платформенной реализацией .NET.</span><span class="sxs-lookup"><span data-stu-id="fe29d-109">The first version of .NET Core (released in 2016) was a single, lightweight, modern, and cross-platform implementation of .NET.</span></span> <span data-ttu-id="fe29d-110">Устаревшие интерфейсы API и API с более современными альтернативными вариантами были намеренно удалены.</span><span class="sxs-lookup"><span data-stu-id="fe29d-110">Obsolete APIs and APIs with more modern alternatives were intentionally removed.</span></span> <span data-ttu-id="fe29d-111">ADO.NET не включал какие-либо интерфейсы API набора данных (включая DataTable и DataAdapter).</span><span class="sxs-lookup"><span data-stu-id="fe29d-111">ADO.NET didn't include any of the DataSet APIs (including DataTable and DataAdapter).</span></span>

<span data-ttu-id="fe29d-112">Группа Entity Framework была в некоторой степени знакома с базой кода System. Data. SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-112">The Entity Framework team was somewhat familiar with the System.Data.SQLite codebase.</span></span> <span data-ttu-id="fe29d-113">Брице Ламбсон, участник команды EF, ранее помогал команде SQLite добавить поддержку Entity Framework версий 5 и 6.</span><span class="sxs-lookup"><span data-stu-id="fe29d-113">Brice Lambson, a member of the EF team, had previously helped the SQLite team add support for Entity Framework versions 5 and 6.</span></span> <span data-ttu-id="fe29d-114">Брице также поэкспериментировать с собственной реализацией поставщика SQLite ADO.NET в то же время, когда планируется выполнение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe29d-114">Brice was also experimenting with his own implementation of a SQLite ADO.NET provider around the same time that .NET Core was being planned.</span></span> <span data-ttu-id="fe29d-115">После длительного обсуждения Группа Entity Framework решила создать Microsoft. Data. SQLite на основе прототипа Брице.</span><span class="sxs-lookup"><span data-stu-id="fe29d-115">After a long discussion, the Entity Framework team decided to create Microsoft.Data.Sqlite based on Brice's prototype.</span></span> <span data-ttu-id="fe29d-116">Это позволит им создавать новые упрощенные и современные реализации, которые будут согласованы с целями .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe29d-116">This would allow them to create a new lightweight and modern implementation that would align with the goals of .NET Core.</span></span>

<span data-ttu-id="fe29d-117">В качестве примера того, что мы имеем в виду более современных, здесь приведен код для создания [определяемой пользователем функции](user-defined-functions.md) в System. Data. SQLite и Microsoft. Data. SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-117">As an example of what we mean by more modern, here is code to create a [user-defined function](user-defined-functions.md) in both System.Data.SQLite and Microsoft.Data.Sqlite.</span></span>

```csharp
// System.Data.SQLite
connection.BindFunction(
    new SQLiteFunctionAttribute("ceiling", 1, FunctionType.Scalar),
    (Func<object[], object>)((object[] args) => Math.Ceiling((double)((object[])args[1])[0])),
    null);

// Microsoft.Data.Sqlite
connection.CreateFunction(
    "ceiling",
    (double arg) => Math.Ceiling(arg));
```

<span data-ttu-id="fe29d-118">В 2017 .NET Core 2,0 изменила стратегию.</span><span class="sxs-lookup"><span data-stu-id="fe29d-118">In 2017, .NET Core 2.0 experienced a change in strategy.</span></span> <span data-ttu-id="fe29d-119">Было принято решение о том, что совместимость с .NET Framework была крайне важной для успешной работы .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe29d-119">It was decided that compatibility with .NET Framework was vital to the success of .NET Core.</span></span> <span data-ttu-id="fe29d-120">Многие из удаленных API, включая API набора данных, были добавлены обратно.</span><span class="sxs-lookup"><span data-stu-id="fe29d-120">Many of the removed APIs, including the DataSet APIs, were added back.</span></span> <span data-ttu-id="fe29d-121">Как и для многих других, этот незаблокированный компонент System. Data. SQLite также позволяет перенести его в .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe29d-121">Like it did for many others, this unblocked System.Data.SQLite allowing it to also be ported to .NET Core.</span></span> <span data-ttu-id="fe29d-122">Исходная цель Microsoft. Data. SQLite — облегченная и современная, однако все еще остается.</span><span class="sxs-lookup"><span data-stu-id="fe29d-122">The original goal of Microsoft.Data.Sqlite to be lightweight and modern, however, still remains.</span></span> <span data-ttu-id="fe29d-123">Дополнительные сведения об интерфейсах API ADO.NET, не реализованных в Microsoft. Data. SQLite, см. в разделе [ограничения ADO.NET](adonet-limitations.md) .</span><span class="sxs-lookup"><span data-stu-id="fe29d-123">See [ADO.NET limitations](adonet-limitations.md) for details about ADO.NET APIs not implemented by Microsoft.Data.Sqlite.</span></span>

<span data-ttu-id="fe29d-124">При добавлении новых функций в Microsoft. Data. SQLite учитывается структура System. Data. SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-124">When new features are added to Microsoft.Data.Sqlite, the design of System.Data.SQLite is taken into account.</span></span> <span data-ttu-id="fe29d-125">Мы пытаемся, по возможности, уменьшить изменения между двумя, чтобы упростить переход между ними.</span><span class="sxs-lookup"><span data-stu-id="fe29d-125">We try, when possible, to minimize changes between the two to ease transitioning between them.</span></span>

## <a name="data-types"></a><span data-ttu-id="fe29d-126">Типы данных</span><span class="sxs-lookup"><span data-stu-id="fe29d-126">Data types</span></span>

<span data-ttu-id="fe29d-127">Крупнейшим различием между Microsoft. Data. SQLite и System. Data. SQLite является обработка типов данных.</span><span class="sxs-lookup"><span data-stu-id="fe29d-127">The biggest difference between Microsoft.Data.Sqlite and System.Data.SQLite is how data types are handled.</span></span> <span data-ttu-id="fe29d-128">Как описано в разделе [типы данных](types.md), Microsoft. Data. SQLite не пытается скрыть базовую разрешающую часть SQLite, что позволяет указать любую произвольную строку в качестве типа столбца и имеет четыре примитивных типа: integer, Real, Text и BLOB.</span><span class="sxs-lookup"><span data-stu-id="fe29d-128">As described in [Data types](types.md), Microsoft.Data.Sqlite doesn't try to hide the underlying quirkiness of SQLite, which allows any arbitrary string to be specified as the column type, and only has four primitive types: INTEGER, REAL, TEXT, and BLOB.</span></span>

<span data-ttu-id="fe29d-129">System. Data. SQLite применяет дополнительную семантику к типам столбцов, сопоставляя их непосредственно с типами .NET.</span><span class="sxs-lookup"><span data-stu-id="fe29d-129">System.Data.SQLite applies additional semantics to column types mapping them directly to .NET types.</span></span> <span data-ttu-id="fe29d-130">Это дает поставщику более строго типизированное поведение, но имеет некоторые грубые края.</span><span class="sxs-lookup"><span data-stu-id="fe29d-130">This gives the provider a more strongly typed feel, but it has some rough edges.</span></span> <span data-ttu-id="fe29d-131">Например, им пришлось ввести новую инструкцию SQL (типы), чтобы указать типы столбцов выражений в инструкциях SELECT.</span><span class="sxs-lookup"><span data-stu-id="fe29d-131">For example, they had to introduce a new SQL statement (TYPES) to specify the column types of expressions in SELECT statements.</span></span>

## <a name="connection-strings"></a><span data-ttu-id="fe29d-132">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe29d-132">Connection strings</span></span>

<span data-ttu-id="fe29d-133">Microsoft. Data. SQLite имеет гораздо меньше ключевых слов [строки подключения](connection-strings.md) .</span><span class="sxs-lookup"><span data-stu-id="fe29d-133">Microsoft.Data.Sqlite has a lot fewer [connection string](connection-strings.md) keywords.</span></span> <span data-ttu-id="fe29d-134">В следующей таблице показаны альтернативные варианты, которые можно использовать вместо.</span><span class="sxs-lookup"><span data-stu-id="fe29d-134">The following table shows alternatives that can be used instead.</span></span>

| <span data-ttu-id="fe29d-135">Ключевое слово</span><span class="sxs-lookup"><span data-stu-id="fe29d-135">Keyword</span></span>          | <span data-ttu-id="fe29d-136">Альтернатива</span><span class="sxs-lookup"><span data-stu-id="fe29d-136">Alternative</span></span>                                         |
| ---------------- | --------------------------------------------------- |
| <span data-ttu-id="fe29d-137">Размер кэша</span><span class="sxs-lookup"><span data-stu-id="fe29d-137">Cache Size</span></span>       | <span data-ttu-id="fe29d-138">Отправить `PRAGMA cache_size = <pages>`</span><span class="sxs-lookup"><span data-stu-id="fe29d-138">Send `PRAGMA cache_size = <pages>`</span></span>                  |
| <span data-ttu-id="fe29d-139">Время ожидания по умолчанию</span><span class="sxs-lookup"><span data-stu-id="fe29d-139">Default Timeout</span></span>  | <span data-ttu-id="fe29d-140">Использование свойства DefaultTimeout в Склитеконнектион</span><span class="sxs-lookup"><span data-stu-id="fe29d-140">Use the DefaultTimeout property on SqliteConnection</span></span> |
| <span data-ttu-id="fe29d-141">фаилифмиссинг</span><span class="sxs-lookup"><span data-stu-id="fe29d-141">FailIfMissing</span></span>    | <span data-ttu-id="fe29d-142">Использование `Mode=ReadWrite`</span><span class="sxs-lookup"><span data-stu-id="fe29d-142">Use `Mode=ReadWrite`</span></span>                                |
| <span data-ttu-id="fe29d-143">фуллури</span><span class="sxs-lookup"><span data-stu-id="fe29d-143">FullUri</span></span>          | <span data-ttu-id="fe29d-144">Использование ключевого слова источника данных</span><span class="sxs-lookup"><span data-stu-id="fe29d-144">Use the Data Source keyword</span></span>                         |
| <span data-ttu-id="fe29d-145">Режим ведения журнала</span><span class="sxs-lookup"><span data-stu-id="fe29d-145">Journal Mode</span></span>     | <span data-ttu-id="fe29d-146">Отправить `PRAGMA journal_mode = <mode>`</span><span class="sxs-lookup"><span data-stu-id="fe29d-146">Send `PRAGMA journal_mode = <mode>`</span></span>                 |
| <span data-ttu-id="fe29d-147">Формат прежних версий</span><span class="sxs-lookup"><span data-stu-id="fe29d-147">Legacy Format</span></span>    | <span data-ttu-id="fe29d-148">Отправить `PRAGMA legacy_file_format = 1`</span><span class="sxs-lookup"><span data-stu-id="fe29d-148">Send `PRAGMA legacy_file_format = 1`</span></span>                |
| <span data-ttu-id="fe29d-149">Максимальное число страниц</span><span class="sxs-lookup"><span data-stu-id="fe29d-149">Max Page Count</span></span>   | <span data-ttu-id="fe29d-150">Отправить `PRAGMA max_page_count = <pages>`</span><span class="sxs-lookup"><span data-stu-id="fe29d-150">Send `PRAGMA max_page_count = <pages>`</span></span>              |
| <span data-ttu-id="fe29d-151">Размер страницы</span><span class="sxs-lookup"><span data-stu-id="fe29d-151">Page Size</span></span>        | <span data-ttu-id="fe29d-152">Отправить `PRAGMA page_size = <bytes>`</span><span class="sxs-lookup"><span data-stu-id="fe29d-152">Send `PRAGMA page_size = <bytes>`</span></span>                   |
| <span data-ttu-id="fe29d-153">Только чтение</span><span class="sxs-lookup"><span data-stu-id="fe29d-153">Read Only</span></span>        | <span data-ttu-id="fe29d-154">Использование `Mode=ReadOnly`</span><span class="sxs-lookup"><span data-stu-id="fe29d-154">Use `Mode=ReadOnly`</span></span>                                 |
| <span data-ttu-id="fe29d-155">Synchronous</span><span class="sxs-lookup"><span data-stu-id="fe29d-155">Synchronous</span></span>      | <span data-ttu-id="fe29d-156">Отправить `PRAGMA synchronous = <mode>`</span><span class="sxs-lookup"><span data-stu-id="fe29d-156">Send `PRAGMA synchronous = <mode>`</span></span>                  |
| <span data-ttu-id="fe29d-157">URI-код</span><span class="sxs-lookup"><span data-stu-id="fe29d-157">Uri</span></span>              | <span data-ttu-id="fe29d-158">Использование ключевого слова источника данных</span><span class="sxs-lookup"><span data-stu-id="fe29d-158">Use the Data Source keyword</span></span>                         |
| <span data-ttu-id="fe29d-159">UseUTF16Encoding</span><span class="sxs-lookup"><span data-stu-id="fe29d-159">UseUTF16Encoding</span></span> | <span data-ttu-id="fe29d-160">Отправить `PRAGMA encoding = 'UTF-16'`</span><span class="sxs-lookup"><span data-stu-id="fe29d-160">Send `PRAGMA encoding = 'UTF-16'`</span></span>                   |

## <a name="authorization"></a><span data-ttu-id="fe29d-161">Авторизация</span><span class="sxs-lookup"><span data-stu-id="fe29d-161">Authorization</span></span>

<span data-ttu-id="fe29d-162">Microsoft. Data. SQLite не имеет API, предоставляющего обратный вызов авторизации SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-162">Microsoft.Data.Sqlite doesn't have any API exposing SQLite's authorization callback.</span></span> <span data-ttu-id="fe29d-163">Чтобы отправить отзыв об этой функции, используйте [#13835](https://github.com/dotnet/efcore/issues/13835) выпуска.</span><span class="sxs-lookup"><span data-stu-id="fe29d-163">Use issue [#13835](https://github.com/dotnet/efcore/issues/13835) to provide feedback about this feature.</span></span>

## <a name="data-change-notifications"></a><span data-ttu-id="fe29d-164">Уведомления об изменении данных</span><span class="sxs-lookup"><span data-stu-id="fe29d-164">Data change notifications</span></span>

<span data-ttu-id="fe29d-165">Microsoft. Data. SQLite не имеет интерфейсов API, предоставляя уведомления об изменении данных SQLite.</span><span class="sxs-lookup"><span data-stu-id="fe29d-165">Microsoft.Data.Sqlite doesn't have any API exposing SQLite's data change notifications.</span></span> <span data-ttu-id="fe29d-166">Чтобы отправить отзыв об этой функции, используйте [#13827](https://github.com/dotnet/efcore/issues/13827) выпуска.</span><span class="sxs-lookup"><span data-stu-id="fe29d-166">Use issue [#13827](https://github.com/dotnet/efcore/issues/13827) to provide feedback about this feature.</span></span>

## <a name="virtual-table-modules"></a><span data-ttu-id="fe29d-167">Модули виртуальной таблицы</span><span class="sxs-lookup"><span data-stu-id="fe29d-167">Virtual table modules</span></span>

<span data-ttu-id="fe29d-168">Microsoft. Data. SQLite не имеет API для создания виртуальных модулей таблиц.</span><span class="sxs-lookup"><span data-stu-id="fe29d-168">Microsoft.Data.Sqlite doesn't have any API for creating virtual table modules.</span></span> <span data-ttu-id="fe29d-169">Чтобы отправить отзыв об этой функции, используйте [#13823](https://github.com/dotnet/efcore/issues/13823) выпуска.</span><span class="sxs-lookup"><span data-stu-id="fe29d-169">Use issue [#13823](https://github.com/dotnet/efcore/issues/13823) to provide feedback about this feature.</span></span>

## <a name="see-also"></a><span data-ttu-id="fe29d-170">См. также:</span><span class="sxs-lookup"><span data-stu-id="fe29d-170">See also</span></span>

* [<span data-ttu-id="fe29d-171">Типы данных</span><span class="sxs-lookup"><span data-stu-id="fe29d-171">Data types</span></span>](types.md)
* [<span data-ttu-id="fe29d-172">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe29d-172">Connection strings</span></span>](connection-strings.md)
* [<span data-ttu-id="fe29d-173">Шифрование</span><span class="sxs-lookup"><span data-stu-id="fe29d-173">Encryption</span></span>](encryption.md)
* [<span data-ttu-id="fe29d-174">Ограничения ADO.NET</span><span class="sxs-lookup"><span data-stu-id="fe29d-174">ADO.NET limitations</span></span>](adonet-limitations.md)
* [<span data-ttu-id="fe29d-175">Ограничения Dapper</span><span class="sxs-lookup"><span data-stu-id="fe29d-175">Dapper limitations</span></span>](dapper-limitations.md)