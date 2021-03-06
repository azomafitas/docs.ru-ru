---
title: Практическое руководство. Задание привязки службы в конфигурации
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885037f7-1c2b-4d7a-90d9-06b89be172f2
ms.openlocfilehash: 245fe50ed5a80c51163652defb642cebefd55dbd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184021"
---
# <a name="how-to-specify-a-service-binding-in-configuration"></a>Практическое руководство. Задание привязки службы в конфигурации
В этом примере контракт `ICalculator` определен для базовой службы калькулятора, служба реализуется в классе `CalculatorService`, а затем ее конечная точка настраивается в файле Web.config с указанием того, что служба использует класс <xref:System.ServiceModel.BasicHttpBinding>. Для описания того, как настроить эту службу с помощью кода, а не конфигурации, [см.](how-to-specify-a-service-binding-in-code.md)  
  
 В большинстве случаев рекомендуется указывать привязку и адрес декларативно в конфигурации, а не принудительно в коде. Как правило, определять конечные точки в коде непрактично, поскольку привязки и адреса для развернутой службы чаще всего отличаются от привязок и адресов, используемых в процессе разработки службы. В общем случае, если не указывать привязку и адрес в коде, их можно изменять без повторной компиляции или повторного развертывания приложения.  
  
 Все следующие шаги конфигурации могут быть предприняты с помощью [инструмента редактора конфигурации (SvcConfigEditor.exe).](configuration-editor-tool-svcconfigeditor-exe.md)  
  
 Для исходной копии этого примера см. [BasicBinding](./samples/basicbinding.md).  
  
## <a name="to-specify-the-basichttpbinding-to-use-to-configure-the-service"></a>Указание привязки BasicHttpBinding, используемой для настройки службы  
  
1. Определите контракт службы для данного типа службы.  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#1)]  
  
2. Реализуйте контракт службы в классе службы.  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#2)]  
  
    > [!NOTE]
    > Информация об адресе или привязке не указывается внутри реализации службы. Кроме того, для извлечения этих сведений из файла конфигурации не требуется писать код.  
  
3. Создайте файл Web.config для настройки конечной точки для `CalculatorService`, использующей <xref:System.ServiceModel.WSHttpBinding>.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name=" CalculatorService" >  

            <!-- Leave the address blank to be populated by default -->
            <!-- from the hosting environment,in this case IIS, so -->
            <!-- the address will just be that of the IIS Virtual -->
            <!-- Directory. -->

            <!-- Specify the binding configuration name for that -->
            <!-- binding type. This is optional but useful if you -->
            <!-- want to modify the properties of the binding. -->
            <!-- The bindingConfiguration name Binding1 is defined -->
            <!-- below in the bindings element. -->
            <endpoint
                address=""
                binding="wsHttpBinding"  
                bindingConfiguration="Binding1"  
                contract="ICalculator" />  
          </service>  
        </services>  
        <bindings>  
          <wsHttpBinding>  
            <binding name="Binding1">  
              <!-- Binding property values can be modified here. -->  
              <!-- See the next procedure. -->  
            </binding>  
          </wsHttpBinding>  
       </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4. Создайте файл Service.svc, содержащий следующую строку, и поместите его в виртуальный каталог IIS.  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>
    ```  
  
## <a name="to-modify-the-default-values-of-the-binding-properties"></a>Изменение значений по умолчанию для свойств привязки  
  
1. Чтобы изменить одно из значений <xref:System.ServiceModel.WSHttpBinding>свойств по умолчанию, `<binding name="Binding1">` создайте новое имя связывающей конфигурации - в элементе [ \<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) и установите новые значения для атрибутов привязки в этом связывающем элементе. Например, чтобы изменить значения по умолчанию для времени ожидания при открытии и закрытии с 1 минуты на 2 минуты, добавьте следующие строки в файл конфигурации.  
  
    ```xml  
    <wsHttpBinding>  
      <binding name="Binding1"  
               closeTimeout="00:02:00"  
               openTimeout="00:02:00">  
      </binding>  
    </wsHttpBinding>  
    ```  
  
## <a name="see-also"></a>См. также раздел

- [Использование привязок для настройки служб и клиентов](using-bindings-to-configure-services-and-clients.md)
- [Указание адреса конечной точки](specifying-an-endpoint-address.md)
