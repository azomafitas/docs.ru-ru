---
title: Метод ICorDebugFunction3::GetActiveReJitRequestILCode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugFunction3.GetActiveReJitRequestILCode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 88584574-ade5-45b2-9778-489ed5c4dd7f
topic_type:
- apiref
ms.openlocfilehash: 9e7f682752cfefae63b574655a4fc5e8964146a0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213183"
---
# <a name="icordebugfunction3getactiverejitrequestilcode-method"></a>Метод ICorDebugFunction3::GetActiveReJitRequestILCode
[Поддерживается в .NET Framework 4.5.2 и более поздних версиях.]  
  
 Возвращает указатель интерфейса на [икордебугилкоде](icordebugilcode-interface.md) , содержащий Il из активного запроса ReJIT.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp
HRESULT GetActiveReJitRequestILCode(  
   ICorDebugILCode **ppReJitedILCode  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `ppReJitedILCode`  
 Указатель на промежуточный язык из активного запроса ReJIT.  
  
## <a name="remarks"></a>Remarks  
 Если метод, представленный этим объектом `ICorDebugFunction3`, имеет активный запрос ReJIT, `ppReJitedILCode` возвращает указатель на его промежуточный язык. Если нет активного запроса, то есть общего случая, то `ppReJitedILCode` имеет **значение NULL**.  
  
 Запрос ReJIT активируется сразу после того, как выполнение возвращается из вызова метода [ICorProfilerCallback4:: жетрежитпараметерс](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-getrejitparameters-method.md) . Он еще не быть может скомпилирован JIT, а потоки могут по-прежнему выполняться в исходной версии кода. Во время вызова профилировщиком метода [метод icorprofilerinfo4:: рекуестреверт](../profiling/icorprofilerinfo4-requestrevert-method.md) запрос ReJIT станет неактивным. Даже после возврата промежуточного языка поток может все еще выполняться в коде, перекомпилированном JIT (ReJIT).  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorDebugFunction3](icordebugfunction3-interface.md)
- [Интерфейсы отладки](debugging-interfaces.md)
- [ReJIT: руководство](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)
