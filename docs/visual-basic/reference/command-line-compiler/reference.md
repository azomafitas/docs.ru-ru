---
title: -reference
ms.date: 03/13/2018
helpviewer_keywords:
- /reference compiler option [Visual Basic]
- r compiler option [Visual Basic]
- -reference compiler option [Visual Basic]
- /r compiler option [Visual Basic]
- reference compiler option [Visual Basic]
- -r compiler option [Visual Basic]
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
ms.openlocfilehash: 35e02d1ad4409e754c2466f7d0ae7e68214772e6
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716703"
---
# <a name="-reference-visual-basic"></a>-reference (Visual Basic)
Дает компилятору указание сделать всю информацию о типах из указанных сборок доступной компилируемому проекту.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-reference:fileList  
```

or

```console
-r:fileList  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`fileList`|Обязательный. Список всех имен файлов сборки, разделенных запятыми. Если имя файла содержит пробел, заключите его в кавычки.|  
  
## <a name="remarks"></a>Примечания  
 Импортируемые файлы должны содержать метаданные сборки. За пределами сборки видны только открытые типы. Параметр [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) импортирует метаданные из модуля.  
  
 При ссылке на сборку (сборка А), которая, в свою очередь, ссылается на другую сборку (сборка Б), необходимо ссылаться на сборку Б в следующих случаях.  
  
- Тип из сборки A наследуется из типа или реализует интерфейс сборки Б.  
  
- Вызывается поле, свойство, событие или метод, имеющий тип возвращаемого значения или тип параметра из сборки Б.  
  
 Для указания каталога, в котором находятся одна или несколько ссылок на сборки, используется параметр [-libpath](../../../visual-basic/reference/command-line-compiler/libpath.md).  
  
 Чтобы компилятор распознал тип в сборке (а не модуль), необходимо принудительно разрешить тип. Это можно сделать различными способами, например, определив экземпляр типа. Существуют другие способы разрешения имен типов в сборке для компилятора. Например, при наследовании от типа в сборке имя типа будет станет известно компилятору.  
  
 По умолчанию используется файл ответов Vbc.rsp, который ссылается на часто используемые сборки .NET Framework. Параметр `-noconfig` позволяет запретить компилятору использовать файл Vbc.rsp.  
  
 Краткой формой `-reference` является `-r`.  
  
## <a name="example"></a>Пример  
 Следующая команда компилирует исходный файл `Input.vb` и ссылочные сборки из `Metad1.dll` и `Metad2.dll` и создает файл `Out.exe`.  
  
```console
vbc -reference:metad1.dll,metad2.dll -out:out.exe input.vb  
```  
  
## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
