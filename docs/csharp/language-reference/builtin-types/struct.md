---
title: Типы структур — справочник по C#
ms.date: 04/21/2020
f1_keywords:
- struct_CSharpKeyword
helpviewer_keywords:
- struct keyword [C#]
- struct type [C#]
- structure type [C#]
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
ms.openlocfilehash: dbe9b47625589de834b7a8021640885ca0920b96
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "82021275"
---
# <a name="structure-types-c-reference"></a>Типы структур (справочник по C#)

*Тип структуры*  представляет собой [тип значения](value-types.md), который может инкапсулировать данные и связанные функции. Для определения типа структуры используется ключевое слово `struct`:

[!code-csharp[struct example](snippets/StructType.cs#StructExample)]

Типы структуры имеют *семантики значений*. То есть переменная типа структуры содержит экземпляр этого типа. По умолчанию значения переменных копируются при назначении, передаче аргумента в метод и возврате результата метода. В случае переменной типа структуры копируется экземпляр типа. Дополнительные сведения см. в разделе [Типы значений](value-types.md).

Как правило, типы структуры используются для проектирования небольших ориентированных на данные типов, которые предоставляют минимум поведения или не предоставляют его вовсе. Например, платформа .NET использует типы структуры для представления числа (как [целого](integral-numeric-types.md), так и [вещественного](floating-point-numeric-types.md)), [логического значения](bool.md), [символа Юникода](char.md), [экземпляра времени](xref:System.DateTime). Если вы сконцентрированы на поведении типа, рекомендуется определить [класс](../keywords/class.md). Типы классов имеют *семантики ссылок*. То есть переменная типа класса содержит ссылку на экземпляр этого типа, а не сам экземпляр.

Поскольку типы структуры имеют семантику значений, рекомендуется определять *неизменяемые* типы структуры.

## <a name="readonly-struct"></a>Структура `readonly`

Начиная с C# версии 7.2, чтобы объявить, что тип структуры является неизменяемым, используйте модификатор `readonly`:

[!code-csharp[readonly struct](snippets/StructType.cs#ReadonlyStruct)]

Все элементы данных структуры `readonly` должны быть доступны только для чтения:

- Любое объявление поля должно иметь [`readonly` модификатор](../keywords/readonly.md).
- Все свойства, включая автоматические реализованные, должны быть доступны только для чтения.

Это гарантирует, что ни один из элементов структуры `readonly` не изменит состояние структуры.

> [!NOTE]
> В структуре `readonly` элемент данных изменяемого ссылочного типа по-прежнему может изменять свое собственное состояние. Например, вы не можете заменить экземпляр <xref:System.Collections.Generic.List%601>, но можете добавить в него новые элементы.

## <a name="readonly-instance-members"></a>Члены экземпляров `readonly`

Начиная с C# 8.0, можно также использовать модификатор `readonly`, чтобы объявить, что член экземпляра не изменяет состояние структуры. Если не удается объявить весь тип структуры как `readonly`, используйте модификатор `readonly`, чтобы пометить члены экземпляров, которые не изменяют состояние структуры. В структуре `readonly` каждый член экземпляра неявно является `readonly`.

В члене экземпляра `readonly` невозможно назначать поля экземпляра структуры. Однако член `readonly` может вызвать член, не являющийся `readonly`. В этом случае компилятор создает копию экземпляра структуры и вызывает в ней член, не являющийся `readonly`. В результате исходный экземпляр структуры остается без изменений.

Как правило, модификатор `readonly` применяется к следующим типам элементов экземпляров.

- Методы.

  [!code-csharp[readonly method](snippets/StructType.cs#ReadonlyMethod)]

  Можно также применить модификатор `readonly` к методам, переопределяющим методы, объявленные в <xref:System.Object?displayProperty=nameWithType>.

  [!code-csharp[readonly override](snippets/StructType.cs#ReadonlyOverride)]

- Свойства и индексаторы.

  [!code-csharp[readonly property get](snippets/StructType.cs#ReadonlyProperty)]

  Если необходимо применить модификатор `readonly` к методам доступа свойства или индексатора, примените его в объявлении свойства или индексатора.

  > [!NOTE]
  > Компилятор объявляет метод доступа `get` [автоматически реализуемого свойства](../../programming-guide/classes-and-structs/auto-implemented-properties.md) как `readonly` независимо от наличия модификатора `readonly` в объявлении свойства.

Модификатор `readonly` не применяется к статическим членам типа структуры.

Компилятор может использовать модификатор `readonly` для оптимизации производительности. Дополнительные сведения см. в статье [Написание безопасного и эффективного кода C#](../../write-safe-efficient-code.md).

## <a name="limitations-with-the-design-of-a-structure-type"></a>Ограничения при проектировании типа структуры

При проектировании типа структуры вы будете располагать теми же возможностями, что и для типа [класса](../keywords/class.md), за исключением следующих аспектов:

- Вы не можете объявить конструктор без параметров. Каждый тип структуры уже предоставляет неявный конструктор без параметров, который создает [значение по умолчанию](default-values.md) типа.

- Вы не можете инициализировать поле экземпляра или свойство при его объявлении. Однако можно инициализировать [статическое](../keywords/static.md) поле или поле [константы](../keywords/const.md) или статическое свойство при его объявлении.

- Конструктор типа структуры должен инициализировать все поля экземпляров данного типа.

- Тип структуры не может наследовать от другого типа класса или структуры и не может быть базовым для класса. Однако тип структуры может реализовывать [интерфейсы](../keywords/interface.md).

- Вы не можете объявить [метод завершения](../../programming-guide/classes-and-structs/destructors.md) в типе структуры.

## <a name="instantiation-of-a-structure-type"></a>Создание экземпляра типа структуры

В C# необходимо инициализировать объявленную переменную, прежде чем ее можно будет использовать. Так как переменная типа структуры не может быть `null` (если только это не переменная [типа значения, допускающего значение NULL](nullable-value-types.md)), необходимо создать экземпляр соответствующего типа. Для этого можно использовать несколько способов.

Как правило, экземпляр типа структуры создается посредством вызова соответствующего конструктора с помощью оператора [`new`](../operators/new-operator.md). Каждый тип структуры имеет по крайней мере один конструктор. Это неявный конструктор без параметров, который создает [значение по умолчанию](default-values.md) данного типа. [Выражения значения по умолчанию](../operators/default.md) можно также использовать для создания значения типа по умолчанию.

Если все поля экземпляров типа структуры доступны, можно также создать его экземпляр без оператора `new`. В этом случае необходимо инициализировать все поля экземпляров перед первым использованием экземпляра. Следующий пример показывает, как это сделать:

[!code-csharp[without new](snippets/StructType.cs#WithoutNew)]

В случае [встроенных типов значения](value-types.md#built-in-value-types) используйте соответствующие литералы, чтобы указать значение типа.

## <a name="passing-structure-type-variables-by-reference"></a>Передача переменных типа структуры по ссылке

При передаче переменной типа структуры в метод в качестве аргумента или возврате значения типа структуры из метода копируется весь экземпляр типа структуры. Это может повлиять на производительность кода в высокопроизводительных сценариях, где используются большие типы структуры. Копирования значений можно избежать, передав переменную типа структуры по ссылке. Используйте модификаторы параметра метода [`ref`](../keywords/ref.md#passing-an-argument-by-reference), [`out`](../keywords/out-parameter-modifier.md) или [`in`](../keywords/in-parameter-modifier.md), чтобы указать, что аргумент должен передаваться по ссылке. Чтобы возвратить результат метода по ссылке, используйте [ref returns](../../programming-guide/classes-and-structs/ref-returns.md). Дополнительные сведения см. в статье [Написание безопасного и эффективного кода C#](../../write-safe-efficient-code.md).

## <a name="ref-struct"></a>Структура `ref`

Начиная с C# 7.2 в объявлении типа структуры можно использовать модификатор `ref`. Экземпляры типа структуры `ref` выделяются в стеке и не могут временно перейти в управляемую кучу. Для этого компилятор ограничивает использование типов структуры `ref` следующим образом:

- Структура `ref` не может быть типом элемента массива.
- Структура `ref` не может быть объявленным типом поля класса или структурой, отличной от`ref`.
- Структура `ref` не может реализовывать интерфейсы.
- Структура `ref` не может быть упакована в <xref:System.ValueType?displayProperty=nameWithType> или <xref:System.Object?displayProperty=nameWithType>.
- Структура `ref` не может быть аргументом типа.
- Переменная структуры `ref` не может быть зафиксирована [лямбда-выражением](../../programming-guide/statements-expressions-operators/lambda-expressions.md) или [локальной функцией](../../programming-guide/classes-and-structs/local-functions.md).
- Переменную структуры `ref` нельзя использовать в методе [`async`](../keywords/async.md). Однако переменные структуры `ref` можно использовать в синхронных методах, например в тех, которые возвращают <xref:System.Threading.Tasks.Task> или <xref:System.Threading.Tasks.Task%601>.
- Переменную структуры `ref` нельзя использовать в [итераторах](../../iterators.md).

Как правило, тип структуры `ref` определяется, если требуется тип, который также содержит члены данных типов структуры `ref`:

[!code-csharp[ref struct](snippets/StructType.cs#RefStruct)]

Чтобы объявить структуру `ref` как [`readonly`](#readonly-struct), объедините модификаторы `readonly` и `ref` в объявлении типа (модификатор `readonly` должен предшествовать модификатору `ref`):

[!code-csharp[readonly ref struct](snippets/StructType.cs#ReadonlyRef)]

В .NET примерами структуры `ref` являются <xref:System.Span%601?displayProperty=nameWithType> и <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>.

## <a name="conversions"></a>Преобразования

Для любого типа структуры (за исключением типов [структуры`ref` ](#ref-struct)) существует [упаковка-преобразование и распаковка-преобразование](../../programming-guide/types/boxing-and-unboxing.md) в типы <xref:System.ValueType?displayProperty=nameWithType> и <xref:System.Object?displayProperty=nameWithType> и из них. Существуют упаковка-преобразование и распаковка-преобразование между типом структуры и любым интерфейсом, который он реализует.

## <a name="c-language-specification"></a>Спецификация языка C#

Дополнительные сведения см. в разделе [Структуры](~/_csharplang/spec/structs.md) в [спецификации языка C#](~/_csharplang/spec/introduction.md).

Дополнительные сведения о функциях, появившихся в C# 7.2 и более поздних версиях, см. в следующих заметках о функциях.

- [Структуры только для чтения](~/_csharplang/proposals/csharp-7.2/readonly-ref.md#readonly-structs)
- [Члены экземпляров только для чтения](~/_csharplang/proposals/csharp-8.0/readonly-instance-members.md)
- [Безопасность во время компиляции для типов, схожих с ссылочными](~/_csharplang/proposals/csharp-7.2/span-safety.md)

## <a name="see-also"></a>См. также

- [справочник по C#](../index.md)
- [Рекомендации по проектированию — выбор между классом и структурой](../../../standard/design-guidelines/choosing-between-class-and-struct.md)
- [Рекомендации по проектированию — проектирование структуры](../../../standard/design-guidelines/struct.md)
- [Классы и структуры](../../programming-guide/classes-and-structs/index.md)
