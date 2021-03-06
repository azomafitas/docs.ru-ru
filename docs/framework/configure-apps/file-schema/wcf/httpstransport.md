---
title: <httpsTransport>
ms.date: 03/30/2017
ms.assetid: f6ed4bc0-7e38-4348-9259-30bf61eb9435
ms.openlocfilehash: 09b0b8500ca93649c814c00739210343bfe1424c
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73739021"
---
# <a name="httpstransport"></a>\<Хттпстранспорт >
Задает транспорт HTTP для передачи сообщений протокола SOAP для пользовательской привязки.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
привязки &nbsp;&nbsp;&nbsp;&nbsp;[ **\<** ](bindings.md) >
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Binding** >\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<хттпстранспорт >**  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<httpsTransport allowCookies="Boolean"
                authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"
                bypassProxyOnLocal="Boolean"
                hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"
                manualAddressing="Boolean"
                maxBufferPoolSize="Integer"
                maxBufferSize="Integer"
                maxReceivedMessageSize="Integer"
                proxyAddress="Uri"
                proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"
                realm="String"
                requireClientCertificate="Boolean"
                transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
                unsafeConnectionNtlmAuthentication="Boolean"
                useDefaultWebProxy="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|allowCookies|Логическое значение, указывающее, принимает ли клиент файлы cookie и распространяет ли он их на будущие запросы. Значение по умолчанию: `false`.<br /><br /> Этот атрибут можно использовать при взаимодействии с веб-службами ASMX, которые используют файлы Cookie. В этом случае можно быть уверенным, что файлы cookie, возвращаемые с сервера, автоматически копируются во все последующие клиентские запросы к этой службе.|  
|authenticationScheme|Задает протокол, используемый для проверки подлинности клиентских запросов, обрабатываемых прослушивателем HTTP. Допустимы следующие значения:<br /><br /> -Digest: указывает дайджест-проверку подлинности.<br />-Negotiate: согласовывается с клиентом для определения схемы проверки подлинности. Если и клиент, и сервер поддерживают Kerberos, используется именно этот протокол; в противном случае используется NTLM.<br />-NTLM: указывает проверку подлинности NTLM.<br />-Basic: указывает обычную проверку подлинности.<br />Анонимный. Указывает анонимную проверку подлинности.<br /><br /> Значение по умолчанию - Anonymous. Это атрибут типа <xref:System.Net.AuthenticationSchemes>. Этот атрибут может быть задан лишь один раз.|  
|bypassProxyOnLocal|Логическое значение, определяющее, будет ли выполняться обход прокси-сервера для локальных адресов. Значение по умолчанию: `false`.<br /><br /> Локальный адрес — это адрес, находящийся в локальной сети или в интрасети.<br /><br /> Windows Communication Foundation (WCF) всегда пропускает прокси-сервер, если адрес службы начинается с `http://localhost`.<br /><br /> Следует использовать имя узла (а не localhost), если необходимо, чтобы клиенты проходили через прокси при взаимодействии со службами на том же компьютере.|  
|hostnameComparisonMode|Задает режим сравнения имен узлов HTTP для анализа универсальных кодов ресурсов (URI). Допустимы следующие значения:<br /><br /> -StrongWildcard: ("+") соответствует всем возможным именам узлов в контексте указанной схемы, порта и относительного URI.<br />-СОВПАД: нет подстановочных знаков<br />-Веаквилдкард: ("\*") соответствует всем возможным именам узлов в контексте указанной схемы, порта и относительных УИР, которые не совпали явным образом или с помощью механизма строгих подстановочных знаков.<br /><br /> Значение по умолчанию - StrongWildcard. Это атрибут типа `System.ServiceModel.HostnameComparison`.|  
|manualAddressing|Логическое значение, позволяющее пользователю взять на себя управление адресацией сообщений. Это свойство обычно используется в сценариях с маршрутизаторами, в которых приложение определяет, в какое из нескольких назначений должно быть отправлено сообщение.<br /><br /> Если атрибут имеет значение `true`, канал предполагает, что для сообщения уже задан адрес, и не добавляет к нему никаких дополнительных сведений. После этого пользователь может адресовать каждое сообщение по отдельности.<br /><br /> Если атрибут имеет значение `false`, используемый по умолчанию механизм адресации Windows Communication Foundation (WCF) автоматически создает адреса для всех сообщений.<br /><br /> Значение по умолчанию: `false`.|  
|maxBufferPoolSize|Положительное целое число, указывающее максимальный размер буферного пула. Значение по умолчанию — 524288.<br /><br /> Многие элементы WCF используют буферы. При создании буферов и их уничтожении после каждого использования расходуется слишком много ресурсов; при сборке мусора для буферов также расходуется слишком много ресурсов. Буферные пулы позволяют брать буфер из пула, использовать его, а затем возвращать обратно, когда он больше не требуется. Это позволяет избежать излишней нагрузки, связанной с созданием и уничтожением буферов.|  
|maxBufferSize|Положительное целое число, указывающее максимальный размер буфера. Значение по умолчанию - 524 288|  
|maxReceivedMessageSize|Положительное целое число, указывающее максимальный допустимый размер сообщения, которое можно получить. Значение по умолчанию — 65536.|  
|proxyAddress|Универсальный код ресурса (URI), задающий адрес прокси-сервера HTTP. Если параметр `useSystemWebProxy` имеет значение `true`, данный параметр должен иметь значение `null`. Значение по умолчанию: `null`.|  
|proxyAuthenticationScheme|Задает протокол, используемый для проверки подлинности клиентских запросов, обрабатываемых прокси-сервером HTTP. Допустимы следующие значения:<br /><br /> -None: проверка подлинности не выполняется.<br />-Digest: указывает дайджест-проверку подлинности.<br />-Negotiate: согласовывается с клиентом для определения схемы проверки подлинности. Если и клиент, и сервер поддерживают Kerberos, используется именно этот протокол; в противном случае используется NTLM.<br />-NTLM: указывает проверку подлинности NTLM.<br />-Basic: указывает обычную проверку подлинности.<br />Анонимный. Указывает анонимную проверку подлинности.<br /><br /> Значение по умолчанию - Anonymous. Это атрибут типа <xref:System.Net.AuthenticationSchemes>. Обратите внимание, что <xref:System.Net.AuthenticationSchemes.IntegratedWindowsAuthentication?displayProperty=nameWithType> не поддерживается.|  
|realm|Строка, задающая область для использования на прокси-сервере. Значение по умолчанию - пустая строка.<br /><br /> Серверы используют области для разделения защищенных ресурсов. Каждый раздел может иметь свою собственную схему проверки подлинности и/или базу данных авторизации. Области используются только для обычной проверки подлинности и дайджест-проверки подлинности. После успешного прохождения клиентом проверки подлинности ее результаты действительны для всех ресурсов в данной области. Подробное описание сфер см. в документе RFC 2617 на [веб-сайте IETF](https://www.ietf.org).|  
|requireClientCertificate|Логическое значение, указывающее, требует ли сервер, чтобы клиент предоставлял сертификат клиента как часть подтверждения HTTPS. Значение по умолчанию: `false`.|  
|transferMode|Указывает, следует ли буферизировать сообщения или передавать их потоком по запросу или ответу. Допустимы следующие значения:<br /><br /> — Буферизовано: сообщения запроса и ответа помещаются в буфер.<br />— Потоковая передача. сообщения запроса и ответа передаются в потоковом режиме.<br />-Стреамедрекуест: сообщение запроса передается в потоковую передачу, а ответное сообщение — в буфер.<br />-Стреамедреспонсе: сообщение запроса буферизовано, а ответное сообщение передается в потоковую передачу.<br /><br /> Значение по умолчанию - Buffered. Это атрибут типа <xref:System.ServiceModel.TransferMode>.|  
|unsafeConnectionNtlmAuthentication|Логическое значение, указывающее, разрешено ли на сервере совместное использование небезопасных подключений. Значение по умолчанию: `false`. Если оно разрешено, проверка подлинности NTLM выполняется один раз для каждого подключения по протоколу TCP.|  
|useDefaultWebProxy|Логическое значение, указывающее, используются ли настройки прокси-сервера компьютера или пользователя. Значение по умолчанию: `true`.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[> привязки \<](bindings.md)|Определяет все возможности пользовательской привязки.|  
  
## <a name="remarks"></a>Заметки  
 Элемент `httpsTransport` является отправной точкой для создания пользовательской привязки, реализующей протокол транспорта HTTPS. HTTPS является основным транспортом, используемым для защиты взаимодействия. Протокол HTTPS поддерживается Windows Communication Foundation (WCF) для обеспечения взаимодействия с другими стеками веб-служб.  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.HttpsTransportElement>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Транспорты](../../../wcf/feature-details/transports.md)
- [Выбор транспорта](../../../wcf/feature-details/choosing-a-transport.md)
- [Привязки](../../../wcf/bindings.md)
- [Расширение привязок](../../../wcf/extending/extending-bindings.md)
- [Пользовательские привязки](../../../wcf/extending/custom-bindings.md)
- [\<customBinding >](custombinding.md)
