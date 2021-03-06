---
title: -libpath
ms.date: 03/10/2018
helpviewer_keywords:
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
ms.openlocfilehash: 9a5822a097828f818da020735c3822e86eb3236b
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716641"
---
# <a name="-libpath"></a>-libpath
Сообщает расположение указанных сборок.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-libpath:dirList  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`dirList`|Обязательный. Разделенный точками с запятой список каталогов, в котором компилятор должен искать сборку, если она отсутствует как в текущем рабочем каталоге (каталоге, из которого был вызван компилятор), так и в системном каталоге среды CLR. Если имя каталога содержит пробел, заключите имя в кавычки (" ").|  
  
## <a name="remarks"></a>Примечания  
 Параметр `-libpath` задает расположение сборок, указанных с помощью параметра [-reference](../../../visual-basic/reference/command-line-compiler/reference.md).  
  
 Компилятор выполняет поиск связанных сборок, для которых не указано полное имя, в следующем порядке:  
  
1. Текущая рабочая папка. Это папка, из которой был вызван компилятор.  
  
2. Системный каталог среды CLR.  
  
3. Каталоги, указанные параметром `-libpath`.  
  
4. Каталоги, указанные переменной среды LIB.  
  
 Параметры `-libpath` является аддитивным; каждое следующее указание этого параметра присоединяется к предыдущим значениям.  
  
 Используйте `-reference` для указания ссылки на сборку.  
  
|Задание -libpath в интегрированной среде разработки Visual Studio|  
|---|  
|1.  Выберите проект в **Обозревателе решений**. В меню **Проект** выберите пункт **Свойства**. <br />2.  Перейдите на вкладку **Ссылки**.<br />3.  Щелкните кнопку **Пути для ссылок...** .<br />4.  В диалоговом окне **Пути для ссылок** введите имя каталога в поле **Folder:** .<br />5.  Щелкните **Добавить папку**.|  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `T2.vb`, чтобы создать файл .exe. Компилятор выполнит поиск ссылок на сборку в рабочем каталоге, корневом каталоге диска С и каталоге "Новые сборки" на диске C:.  
  
```console  
vbc -libpath:c:\;"c:\New Assemblies" -reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>См. также

- [Сборки в .NET](../../../standard/assembly/index.md)
- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
