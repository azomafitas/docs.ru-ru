---
title: Справочник по C#. Целочисленные типы
description: Сведения о диапазоне значений, размере занимаемой памяти и способах использования каждого из целочисленных типов.
ms.date: 06/25/2019
f1_keywords:
- byte
- byte_CSharpKeyword
- sbyte_CSharpKeyword
- sbyte
- short
- short_CSharpKeyword
- ushort
- ushort_CSharpKeyword
- int_CSharpKeyword
- int
- uint
- uint_CSharpKeyword
- long_CSharpKeyword
- long
- ulong_CSharpKeyword
- ulong
helpviewer_keywords:
- integral types, C#
- Visual C#, integral types
- types [C#], integral types
- ranges of integral types [C#]
- byte keyword [C#]
- sbyte keyword [C#]
- short keyword [C#]
- ushort keyword [C#]
- int keyword [C#]
- uint keyword [C#]
- long keyword [C#]
- ulong keyword [C#]
ms.openlocfilehash: dfb1298abaff0cfe8eae7536f94511a30012a4a9
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/16/2019
ms.locfileid: "68236075"
---
# <a name="integral-numeric-types--c-reference"></a>Целочисленные типы (справочник по C#)

**Целочисленные типы** — это подмножество **простых типов**. Они могут инициализироваться [*литералами*](#integral-literals). Кроме того, все целочисленные типы являются типами значений. Все целочисленные типы поддерживают [арифметические](../operators/arithmetic-operators.md) операторы, [побитовые логические](../operators/bitwise-and-shift-operators.md) операторы, операторы [сравнения и равенства](../operators/equality-operators.md).

## <a name="characteristics-of-the-integral-types"></a>Характеристики целочисленных типов

C# поддерживает следующие предварительно определенные целочисленные типы:

|Ключевое слово или тип C#|Диапазон|Размер|Тип .NET|
|----------|-----------|----------|-------------|
|`sbyte`|От -128 до 127|8-разрядное целое число со знаком|<xref:System.SByte?displayProperty=nameWithType>|
|`byte`|От 0 до 255|8-разрядное целое число без знака|<xref:System.Byte?displayProperty=nameWithType>|
|`short`|От -32 768 до 32 767|16-разрядное целое число со знаком|<xref:System.Int16?displayProperty=nameWithType>|
|`ushort`|От 0 до 65 535|16-разрядное целое число без знака|<xref:System.UInt16?displayProperty=nameWithType>|
|`int`|От -2 147 483 648 до 2 147 483 647|32-разрядное целое число со знаком|<xref:System.Int32?displayProperty=nameWithType>|
|`uint`|От 0 до 4 294 967 295|32-разрядное целое число без знака|<xref:System.UInt32?displayProperty=nameWithType>|
|`long`|От -9 223 372 036 854 775 808 до 9 223 372 036 854 775 807|64-разрядное целое число со знаком|<xref:System.Int64?displayProperty=nameWithType>|
|`ulong`|От 0 до 18 446 744 073 709 551 615|64-разрядное целое число без знака|<xref:System.UInt64?displayProperty=nameWithType>|

В приведенной выше таблице каждый тип ключевого слова C# из крайнего левого столбца является псевдонимом для соответствующего типа .NET. Они взаимозаменяемые. Например, следующие объявления объявляют переменные одного типа:

```csharp
int a = 123;
System.Int32 b = 123;
```

По умолчанию все целочисленные типы имеют значение `0`. Все целочисленные типы имеют константы `MinValue` и `MaxValue` с минимальным и максимальными итоговыми значениями этого типа.

Используйте структуру <xref:System.Numerics.BigInteger?displayProperty=nameWithType>, чтобы представить целое число со знаком без верхней и нижней границ.

## <a name="integral-literals"></a>Целочисленные литералы

Целочисленные литералы можно задать как *десятичные*, *шестнадцатеричные* или *двоичные литералы*. Ниже приведены примеры каждого из них:

```csharp
var decimalLiteral = 42;
var hexLiteral = 0x2A;
var binaryLiteral = 0b_0010_1010;
```

Десятичные литералы не требуют префикса. Префикс `x` или `X` означает, что это *шестнадцатеричный литерал*. Префикс `b` или `B` означает, что это *двоичный литерал*. Объявление `binaryLiteral` демонстрирует использование символа `_` в качестве *разделителя разрядов*. Разделитель разрядов можно использовать с любыми числовыми литералами. Двоичные литералы и разделитель разрядов `_` поддерживаются начиная с C# 7.0.

### <a name="literal-suffixes"></a>Суффиксы литералов

Суффикс `l` или `L` указывает, что целочисленный литерал должен иметь тип `long`. Суффикс `ul` или `UL` указывает тип `ulong`. Если суффикс `L` используется с литералом, значение которого больше 9 223 372 036 854 775 807 (максимальное значение типа `long`), литерал преобразуется в тип `ulong`. Если значение, представленное целочисленным литералом, превышает <xref:System.UInt64.MaxValue?displayProperty=nameWithType>, происходит ошибка компиляции [CS1021](../../misc/cs1021.md). 

> [!NOTE]
> Строчную букву "l" можно использовать в качестве суффикса. Однако при этом выдается предупреждение компилятора, так как букву "l" легко перепутать с цифрой "1". Для ясности используйте "L".

### <a name="type-of-an-integral-literal"></a>Тип целочисленного литерала

Если целочисленный литерал не имеет суффикса, его типом будет первый из следующих типов, в котором может быть представлено его значение:

1. `int`
1. `uint`
1. `long`
1. `ulong`

Целочисленный литерал можно преобразовать в тип с меньшим диапазоном, чем у типа по умолчанию, путем присвоения или приведения:

```csharp
byte byteVariable = 42; // type is byte
var signedByte = (sbyte)42; // type is sbyte.
```

Целочисленный литерал можно преобразовать в тип с большим диапазоном, чем у типа по умолчанию, путем присвоения, приведения или добавления суффикса:

```csharp
var unsignedLong = 42UL;
var longVariable = 42L;
ulong anotherUnsignedLong = 42;
var anotherLong = (long)42;
```

## <a name="conversions"></a>Преобразования

Между любыми двумя целочисленными типами, один из которых поддерживает любые значения другого, существует неявное преобразование (которое называется *расширяющим*). Например, существует неявное преобразование из `int` в `long`, так как диапазон значений типа `int` является строгим подмножеством значений `long`. Целочисленный тип без знака меньшего размера может неявно преобразовываться в целочисленный тип со знаком большего размера. Кроме того, существуют неявные преобразования любых целочисленных типов в любые типы с плавающей запятой.  Неявных преобразований целочисленных типов со знаком в целочисленные типы без знака нет.

Если неявное преобразование между двумя целочисленными типами не определено, необходимо использовать явное приведение. Это называется *сужающим преобразованием*. Явное приведение требуется по той причине, что преобразование может привести к потере данных.

## <a name="see-also"></a>См. также

- [Спецификация языка C# — целочисленные типы](~/_csharplang/spec/types.md#integral-types)
- [справочник по C#](../index.md)
- [Типы с плавающей запятой](floating-point-numeric-types.md)
- [Таблица значений по умолчанию](../keywords/default-values-table.md)
- [Таблица форматирования числовых результатов](../keywords/formatting-numeric-results-table.md)
- [Таблица встроенных типов](../keywords/built-in-types-table.md)
- [Числовые значения в .NET](../../../standard/numerics.md)