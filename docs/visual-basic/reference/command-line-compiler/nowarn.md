---
title: -nowarn
ms.date: 07/20/2015
helpviewer_keywords:
- nowarn compiler option [Visual Basic]
- /nowarn compiler option [Visual Basic]
- -nowarn compiler option [Visual Basic]
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
ms.openlocfilehash: 880fdf4931dadea547d64d0506bd3e978956468e
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005400"
---
# <a name="-nowarn"></a>-nowarn
Отключает возможность компилятора создавать предупреждения.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-nowarn[:numberList]  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`numberList`|Необязательный элемент. Разделенный запятыми список с идентификаторами предупреждений, которые должен подавлять компилятор. Если идентификаторы предупреждений не указаны, подавляются все предупреждения.|  
  
## <a name="remarks"></a>Примечания  
 Параметр `-nowarn` указывает компилятору не генерировать предупреждения. Чтобы подавить отдельное предупреждение, укажите идентификатор предупреждения в параметре `-nowarn` после двоеточия. Можно указать несколько кодов предупреждений, разделяя их запятыми.  
  
 Указывайте только числовую часть идентификатора предупреждения. Например, если вы хотите подавить предупреждение BC42024, которое создается для неиспользуемых локальных переменных, укажите `-nowarn:42024`.  
  
 Дополнительные сведения о идентификаторах предупреждений см. в статье [Настройка предупреждений в Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
|Задание параметра -nowarn в интегрированной среде разработки Visual Studio|  
|---|  
|1.  Выберите проект в **Обозревателе решений**. В меню **Проект** выберите пункт **Свойства**. <br />2.  Откройте вкладку **Компиляция**.<br />3.  Установите флажок **Выключить все предупреждения**, чтобы полностью отключить предупреждения.<br />     -или-<br />     Чтобы отключить конкретное предупреждение, выберите **Нет** из раскрывающегося списка рядом с предупреждением.|  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `T2.vb` и не отображает никаких предупреждений.  
  
```console
vbc -nowarn t2.vb  
```  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `T2.vb` и не отображает предупреждений о неиспользуемых локальных переменных (42024).  
  
```console
vbc -nowarn:42024 t2.vb  
```  
  
## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
