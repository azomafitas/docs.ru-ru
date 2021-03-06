---
title: -resource
ms.date: 03/13/2018
helpviewer_keywords:
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
ms.openlocfilehash: a781d543dd32ffb3d0ac0b11c544dbfd8cd5d806
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348557"
---
# <a name="-resource-visual-basic"></a>-resource (Visual Basic)
Внедряет управляемый ресурс в сборку.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-resource:filename[,identifier[,public|private]]  
```

or  

```console
-res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`filename`|Обязательный. Имя файла ресурсов, который вам нужно внедрить в выходной файл. По умолчанию `filename` в сборке является общедоступным. Если имя файла содержит пробел, заключите это имя в кавычки (" ").|  
|`identifier`|Необязательный элемент. Логическое имя ресурса, которое используется для его загрузки. По умолчанию используется имя файла. При необходимости в манифесте сборки можно указать, является ли ресурс общедоступным или частным, например так: `-res:filename.res, myname.res, public`.|  
  
## <a name="remarks"></a>Примечания  
 Используйте `-linkresource`, чтобы связать ресурс со сборкой без размещения файла ресурсов в выходном файле.  
  
 Если `filename` — файл ресурса .NET Framework, созданный генератором файлов ресурсов ([Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md)) или в среде разработки, то к нему можно обращаться с помощью элементов пространства имен <xref:System.Resources> (дополнительные сведения см. в статье о классе <xref:System.Resources.ResourceManager>). Для доступа ко всем остальным ресурсам во время выполнения используйте следующие методы: <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>, <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> и <xref:System.Reflection.Assembly.GetManifestResourceStream%2A>.  
  
 Краткой формой `-resource` является `-res`.  
  
 Дополнительные сведения о настройке `-resource` в интегрированной среде разработки Visual Studio см. в статье [об управлении ресурсами приложения в .NET](/visualstudio/ide/managing-application-resources-dotnet).  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `In.vb` и присоединяет файл ресурсов `Rf.resource`.  
  
```console
vbc -res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)
- [-linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
