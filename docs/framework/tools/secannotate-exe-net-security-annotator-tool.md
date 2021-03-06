---
title: SecAnnotate.exe (средство создания заметок безопасности .NET)
ms.date: 03/30/2017
helpviewer_keywords:
- SecAnnotate.exe
- Security Annotator tool
ms.assetid: 8104d208-7813-4a1d-8a75-58f9a7bcb8c9
ms.openlocfilehash: ffc275c588775fb79da276be904ada90a5a31bad
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2020
ms.locfileid: "75937929"
---
# <a name="secannotateexe-net-security-annotator-tool"></a>SecAnnotate.exe (средство создания заметок безопасности .NET)
Средство создания заметок безопасности .NET Security Annotator (SecAnnotate.exe) — это приложение командной строки, определяющее части `SecurityCritical` и `SecuritySafeCritical` одной или нескольких сборок.  
  
 Расширение Visual Studio [Security Annotator](https://marketplace.visualstudio.com/items?itemName=sheldonb.SecurityAnnotator) обеспечивает графический пользовательский интерфейс для программы SecAnnotate.exe и позволяет запускать эту программу из Visual Studio.  
  
 Это средство автоматически устанавливается с Visual Studio. Чтобы применить этот инструмент, воспользуйтесь командной строкой разработчика для Visual Studio (или командной строкой Visual Studio в Windows 7). Дополнительные сведения см. в разделе [Командные строки](developer-command-prompt-for-vs.md).  
  
 В командной строке введите следующий текст, где *параметры* описаны в следующем разделе, а *сборки* состоят из одного имени сборок или нескольких, разделенных пробелами.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
SecAnnotate.exe [parameters] [assemblies]  
```  
  
## <a name="parameters"></a>Параметры  
  
|Параметр|Описание:|  
|------------|-----------------|  
|`/a`<br /><br /> or<br /><br /> `/showstatistics`|Показывает статистику использования прозрачности в анализируемых сборках.|  
|`/d:` *каталог*<br /><br /> or<br /><br /> `/referencedir:` *каталог*|Указывает каталог для поиска зависимых сборок во время создания заметок.|  
|`/i`<br /><br /> or<br /><br /> `/includesignatures`|Включает данные расширенной подписи в файл отчетов аннотирования.|  
|`/n`<br /><br /> or<br /><br /> `/nogac`|Отключает поиск сборок в глобальном кэше сборок, на которые указывают ссылки.|  
|`/o:` *output.xml*<br /><br /> or<br /><br /> `/out:` *output.xml*|Указывает выходной файл аннотаций.|  
|`/p:` *макс_число_проходов*<br /><br /> or<br /><br /> `/maximumpasses:` *макс_число_проходов*|Задает максимальное число проходов аннотирования, выполняемых для сборок до прекращения создания новых заметок.|  
|`/q`<br /><br /> or<br /><br /> `/quiet`|Задает тихий режим, при котором средство создания заметок безопасности не выводит сообщения о состоянии, а выводит только сведения об ошибке.|  
|`/r:` *сборка*<br /><br /> or<br /><br /> `/referenceassembly:` *сборка*|Включает указанную сборку при разрешении зависимых сборок во время аннотирования. Ссылается на сборки, получающие приоритет над сборками, которые находятся по пути для ссылок.|  
|`/s:` *имя_правила*<br /><br /> or<br /><br /> `/suppressrule:` *имя_правила*|Запрещает выполнение указанного правила прозрачности для входных сборок.|  
|`/t`<br /><br /> or<br /><br /> `/forcetransparent`|Включает режим, при котором средство создания заметок безопасности принудительно считает все сборки, не имеющие никаких заметок о прозрачности, полностью прозрачными.|  
|`/t`:*сборка*<br /><br /> or<br /><br /> `/forcetransparent`:*сборка*|Указанная сборка будет считаться прозрачной независимо от текущих заметок на уровне сборки.|  
|||  
|`/v`<br /><br /> or<br /><br /> `/verify`|Проверяет только правильность заметок сборки, не выполняет несколько проходов для нахождения всех требуемых заметок, если сборка не проверяется.|  
|`/x`<br /><br /> or<br /><br /> `/verbose`|Задает подробный вывод при создании заметок.|  
|`/y:` *каталог*<br /><br /> or<br /><br /> `/symbolpath:` *каталог*|Включает указанный каталог при поиске файлов символов во время аннотирования.|  
  
## <a name="remarks"></a>Remarks  
 Параметры и сборки также могут предоставляться в файле ответов, указанном в командной строке с префиксом в виде знака \@ . Каждая строка в файле ответов должна содержать один параметр или имя сборки.  
  
 Дополнительные сведения о .NET Security Annotator см. в записи [Использование SecAnnotate для анализа сборок на наличие нарушений прозрачности](https://docs.microsoft.com/archive/blogs/shawnfa/using-secannotate-to-analyze-your-assemblies-for-transparency-violations-an-example) в блоге .NET Security.  
  
## <a name="examples"></a>Примеры
