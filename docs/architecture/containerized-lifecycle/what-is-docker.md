---
title: Что такое Docker?
description: Чтобы лучше понять принцип работы Docker, можно воспользоваться простой аналогией.
ms.date: 02/15/2019
ms.openlocfilehash: 7747c4985af27be0a073fad2f22622f697f4ce27
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673431"
---
# <a name="what-is-docker"></a>Что такое Docker?

[Docker](https://www.docker.com/) — это [проект с открытым исходным кодом](https://github.com/docker/docker) для автоматизации развертывания приложений в виде переносимых автономных контейнеров, выполняемых в облаке или локальной среде. Одновременно с этим, Docker — это [компания](https://www.docker.com/), которая разрабатывает и продвигает эту технологию в сотрудничестве с поставщиками облачных служб, а также решений Linux и Windows, включая корпорацию Майкрософт.

![Контейнеры Docker могут работать в любой среде, например в локальном центре обработки данных, в службе стороннего поставщика или в облаке Azure.](./media/image2.png)

**Рис. 1-2**. Docker развертывает контейнеры на всех уровнях гибридного облака

Контейнеры образов Docker работают в исходном формате в Linux и Windows. Но образы Windows будут выполняться только на узлах Windows, тогда как образы Linux — на узлах Linux или Windows (на данный момент с помощью виртуальной машины Linux Hyper-V). Термин "узлы" здесь означает физические серверы и виртуальные машины.

Разработчики могут использовать среды разработки на базе Windows, Linux или macOS. На компьютере разработчика выполняется узел Docker, где развернуты образы Docker с создаваемым приложением и всеми его зависимостями. Разработчики, использующие Linux или Mac, могут применять узел Docker на базе Linux и создавать образы только для контейнеров Linux. (На компьютерах Mac разработчики могут изменять код приложения и запускать в macOS интерфейс командной строки Docker, но на момент написания данной статьи не могут запускать контейнеры непосредственно в macOS.) В Windows разработчики могут создавать образы для контейнеров Linux или Windows.

Docker предоставляет версию [Docker Community Edition (CE)](https://www.docker.com/community-edition) для Windows или macOS, которая позволяет размещать контейнеры в среде разработки и предоставляет дополнительные средства разработки. Оба продукта устанавливают необходимую виртуальную машину (узел Docker) для размещения контейнеров. Docker также предлагает версию [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition), которая предназначена для корпоративных разработчиков и ИТ-отделов, которые создают, распространяют и выполняют крупные и критически важные приложения в рабочей среде.

Для выполнения [контейнеров Windows](/virtualization/windowscontainers/about/) есть среды выполнения двух типов:

- **Контейнеры Windows Server** изолируют приложение с помощью технологии изоляции процесса и пространства имен. Контейнер Windows Server использует ядро совместно с узлом контейнеров и всеми остальными контейнерами на узле.

- **Контейнеры Hyper-V** увеличивают изоляцию, обеспеченную контейнерами Windows Server, запуская каждый контейнер в оптимизированной виртуальной машине. В этой конфигурации ядро узла контейнера не используется совместно с контейнерами Hyper-V, что улучшает изоляцию.

Образы для этих контейнеров создаются и работают одинаково. Различие заключается лишь в том, что для создания контейнера из образа с контейнером Hyper-V нужен дополнительный параметр. Дополнительные сведения см. в разделе [Контейнеры Hyper-V](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/hyperv-container).

## <a name="comparing-docker-containers-with-virtual-machines"></a>Сравнение контейнеров Docker с виртуальными машинами

На рисунке 1-3 показано сравнение между виртуальными машинами и контейнерами Docker.

![Для виртуальных машин на сервере узла создается три базовых уровня: самый нижний инфраструктурный слой; затем операционная система узла и низкоуровневая оболочка; и поверх этого каждая виртуальная машина использует собственную ОС и все необходимые библиотеки. С другой стороны, для Docker сервер узла предоставляет только инфраструктуру и операционную систему, а также ядро контейнеров, которое изолирует контейнер с использованием базовых служб операционной системы.](./media/image3.png)

**Рис. 1-3**. Сравнение традиционных виртуальных машин с контейнерами Docker

Так как контейнеры требуют гораздо меньше ресурсов (например, им не нужна полная ОС), их проще развертывать и они быстрее запускаются. Это позволяет повысить плотность развертываний, то есть запустить на одной единице оборудования больше служб и сократить затраты на них.

Запуск на одном ядре приводит к тому, что уровень изоляции будет ниже, чем на виртуальных машинах.

Основная цель образа — привести среду (зависимости) к единообразию в различных развертываниях. Это означает, что вы можете отладить образ на одном компьютере, а затем развернуть его на другом компьютере и получить ту же среду.

Образ контейнера — это способ упаковки приложения или службы для надежного и воспроизводимого развертывания. Можно сказать, что Docker является не только технологией, но еще философией и процессом.

При работе с Docker разработчики никогда не жалуются, что приложение работает только на локальном компьютере, но не в рабочей среде. Им достаточно сказать "Выполняется в Docker", так как упакованное приложение Docker будет выполняться в любой поддерживаемой среде Docker. Оно будет работать одинаково во всех сценариях развертывания (разработка, контроль качества, промежуточное размещение и рабочая среда).

## <a name="a-simple-analogy"></a>Простая аналогия

Возможно, небольшая аналогия поможет вам быстрее освоить ключевую концепцию Docker.

Вернемся ненадолго назад во времени, в 1950-е годы. Тогда еще не было текстовых редакторов, и повсеместно использовались фотокопировальные устройства (то есть то, что тогда так называлось).

Представьте, что вам понадобилось быстро подготовить наборы писем, чтобы отправить их с обычной бумажной почтой в настоящих конвертах с марками и доставить по домашнему адресу клиента (не забывайте, еще не существует электронной почты).

В какой-то момент вы понимаете, что каждое письмо составлено из широкого набора абзацев, которые выбираются и упорядочиваются по мере необходимости с учетом назначения письма. Вы создаете систему, которая быстро создает нужные письма, и обоснованно надеетесь на существенную прибавку.

Вы создали простую систему со следующим алгоритмом:

1. У вас есть пачка прозрачных листов, каждый из которых содержит один абзац.

2. Чтобы подготовить комплект писем, вы отбираете листы с нужными абзацами, собираете их в стопку и выравниваете так, чтобы все правильно читалось.

3. Теперь вы помещаете готовый набор в фотокопировальное устройство и нажмите кнопку запуска, чтобы изготовить нужное количество копий.

Это и есть основная концепция Docker в упрощенной форме.

В Docker каждый слой представляет некоторый набор изменений, которые применяются к файловой системе после выполнения команды, такой как установка программы.

Если вы "посмотрите" на файловую систему после копирования очередного слоя, вы увидите все файлы в том состоянии, которое они приняли после установки программы.

Такой образ можно рассматривать как дополнительный жесткий диск, доступный только для чтения, который готов к установке на "компьютер" с уже установленной операционной системой.

Соответственно, роль "компьютера" здесь выполняет контейнер, в который устанавливается жесткий диск этого образа. Контейнер, как и обычный компьютер, можно включать и отключать.

>[!div class="step-by-step"]
>[Назад](index.md)
>[Вперед](docker-terminology.md)