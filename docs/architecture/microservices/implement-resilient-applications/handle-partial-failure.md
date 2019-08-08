---
title: Обработка частичного сбоя
description: Узнайте, как правильно обрабатывать частичные сбои. Микрослужба может быть не полностью работоспособной, но при этом выполнять некоторые полезные действия.
ms.date: 10/16/2018
ms.openlocfilehash: a667ad2e1456db7b5846023de27d3797dad58731
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674701"
---
# <a name="handle-partial-failure"></a><span data-ttu-id="c65f1-104">Обработка частичного сбоя</span><span class="sxs-lookup"><span data-stu-id="c65f1-104">Handle partial failure</span></span>

<span data-ttu-id="c65f1-105">В распределенных системах, таких как приложения на базе микрослужб, всегда есть риск частичного сбоя.</span><span class="sxs-lookup"><span data-stu-id="c65f1-105">In distributed systems like microservices-based applications, there's an ever-present risk of partial failure.</span></span> <span data-ttu-id="c65f1-106">Например, одна микрослужба или контейнер могут отказать или не отвечать какое-то время или одна виртуальная машина или сервер могут дать сбой.</span><span class="sxs-lookup"><span data-stu-id="c65f1-106">For instance, a single microservice/container can fail or might not be available to respond for a short time, or a single VM or server can crash.</span></span> <span data-ttu-id="c65f1-107">Поскольку клиенты и службы являются отдельными процессами, служба может не ответить вовремя на запрос клиента.</span><span class="sxs-lookup"><span data-stu-id="c65f1-107">Since clients and services are separate processes, a service might not be able to respond in a timely way to a client’s request.</span></span> <span data-ttu-id="c65f1-108">Служба может быть перегружена, очень медленно отвечать на запросы, быть недоступна некоторое время из-за проблем в сети.</span><span class="sxs-lookup"><span data-stu-id="c65f1-108">The service might be overloaded and responding very slowly to requests or might simply not be accessible for a short time because of network issues.</span></span>

<span data-ttu-id="c65f1-109">Рассмотрим страницу сведений о заказе в примере приложения eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="c65f1-109">For example, consider the Order details page from the eShopOnContainers sample application.</span></span> <span data-ttu-id="c65f1-110">Если микрослужба заказа не отвечает при попытке оформить заказ, в результате неправильного применения клиентского процесса (веб-приложения MVC) — например, если код клиента должен был использовать синхронные RPC без установленного времени ожидания — потоки будут заблокированы в ожидании ответа на неопределенное время.</span><span class="sxs-lookup"><span data-stu-id="c65f1-110">If the ordering microservice is unresponsive when the user tries to submit an order, a bad implementation of the client process (the MVC web application)—for example, if the client code were to use synchronous RPCs with no timeout—would block threads indefinitely waiting for a response.</span></span> <span data-ttu-id="c65f1-111">Помимо того, что это вызывает недовольство пользователей, долгое ожидание занимает или блокирует поток, а потоки очень важны для масштабируемых приложений.</span><span class="sxs-lookup"><span data-stu-id="c65f1-111">Besides creating a bad user experience, every unresponsive wait consumes or blocks a thread, and threads are extremely valuable in highly scalable applications.</span></span> <span data-ttu-id="c65f1-112">Если заблокированных потоков много, в конце концов в среде выполнения приложения их не останется.</span><span class="sxs-lookup"><span data-stu-id="c65f1-112">If there are many blocked threads, eventually the application’s runtime can run out of threads.</span></span> <span data-ttu-id="c65f1-113">В этом случае приложение перестанет отвечать на запросы полностью, а не частично, как показано на рисунке 8-1.</span><span class="sxs-lookup"><span data-stu-id="c65f1-113">In that case, the application can become globally unresponsive instead of just partially unresponsive, as shown in Figure 8-1.</span></span>

![Схема, иллюстрирующая предыдущий абзац](./media/image1.png)

<span data-ttu-id="c65f1-115">**Рис. 8-1**.</span><span class="sxs-lookup"><span data-stu-id="c65f1-115">**Figure 8-1**.</span></span> <span data-ttu-id="c65f1-116">Частичные сбои из-за зависимостей, влияющих на доступность потоков службы</span><span class="sxs-lookup"><span data-stu-id="c65f1-116">Partial failures because of dependencies that impact service thread availability</span></span>

<span data-ttu-id="c65f1-117">В крупных приложениях на базе микрослужб частичные сбои могут быть более масштабными, особенно если взаимодействие с внутренними микрослужбами по большей части основано на синхронных вызовах HTTP (что считается антишаблоном).</span><span class="sxs-lookup"><span data-stu-id="c65f1-117">In a large microservices-based application, any partial failure can be amplified, especially if most of the internal microservices interaction is based on synchronous HTTP calls (which is considered an anti-pattern).</span></span> <span data-ttu-id="c65f1-118">Представьте себе, что система получает миллионы входящих вызовов в день.</span><span class="sxs-lookup"><span data-stu-id="c65f1-118">Think about a system that receives millions of incoming calls per day.</span></span> <span data-ttu-id="c65f1-119">Если система неправильно спроектирована и базируется на длинных цепочках синхронных вызовов HTTP, эти входящие вызовы могут превратиться в еще большее количество исходящих вызовов (предположим, в соотношении 1:4) в десятки внутренних микрослужб в качестве синхронных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c65f1-119">If your system has a bad design that's based on long chains of synchronous HTTP calls, these incoming calls might result in many more millions of outgoing calls (let’s suppose a ratio of 1:4) to dozens of internal microservices as synchronous dependencies.</span></span> <span data-ttu-id="c65f1-120">Рисунок 8-2 иллюстрирует такую ситуацию, в частности зависимость 3.</span><span class="sxs-lookup"><span data-stu-id="c65f1-120">This situation is shown in Figure 8-2, especially dependency \#3.</span></span>

![Неправильно спроектированная микрослужба веб-приложения, зависящая от цепочки зависимостей с другими микрослужбами](./media/image2.png)

<span data-ttu-id="c65f1-122">**Рис. 8-2**.</span><span class="sxs-lookup"><span data-stu-id="c65f1-122">**Figure 8-2**.</span></span> <span data-ttu-id="c65f1-123">Последствия построения неверной конструкции с длинными цепочками HTTP-запросов</span><span class="sxs-lookup"><span data-stu-id="c65f1-123">The impact of having an incorrect design featuring long chains of HTTP requests</span></span>

<span data-ttu-id="c65f1-124">Периодические сбои неизбежны в распределенной и облачной системе, даже если каждая зависимость в отдельности хорошо доступна.</span><span class="sxs-lookup"><span data-stu-id="c65f1-124">Intermittent failure is guaranteed in a distributed and cloud-based system, even if every dependency itself has excellent availability.</span></span> <span data-ttu-id="c65f1-125">Этот факт необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="c65f1-125">It's a fact you need to consider.</span></span>

<span data-ttu-id="c65f1-126">Если вы не разрабатываете и не реализуете меры обеспечения отказоустойчивости, даже небольшие простои могут увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="c65f1-126">If you do not design and implement techniques to ensure fault tolerance, even small downtimes can be amplified.</span></span> <span data-ttu-id="c65f1-127">Например, 50 зависимостей с доступностью 99,99 % — это несколько часов простоя в месяц в результате такого волнового эффекта.</span><span class="sxs-lookup"><span data-stu-id="c65f1-127">As an example, 50 dependencies each with 99.99% of availability would result in several hours of downtime each month because of this ripple effect.</span></span> <span data-ttu-id="c65f1-128">В случае сбоя зависимости от микрослужбы при обработке большого количества запросов этот сбой может заполнить все доступные потоки запросов в каждой службе и привести к отказу всего приложения.</span><span class="sxs-lookup"><span data-stu-id="c65f1-128">When a microservice dependency fails while handling a high volume of requests, that failure can quickly saturate all available request threads in each service and crash the whole application.</span></span>

![Частичные сбои могут значительно усиливаться цепочками зависимостей](./media/image3.png)

<span data-ttu-id="c65f1-130">**Рис. 8-3**.</span><span class="sxs-lookup"><span data-stu-id="c65f1-130">**Figure 8-3**.</span></span> <span data-ttu-id="c65f1-131">Частичный сбой, усиленный микрослужбами с длинными цепочками синхронных вызовов HTTP</span><span class="sxs-lookup"><span data-stu-id="c65f1-131">Partial failure amplified by microservices with long chains of synchronous HTTP calls</span></span>

<span data-ttu-id="c65f1-132">Чтобы свести к минимуму эту проблему, мы рекомендуем использовать асинхронную связь с внутренними микрослужбами, как описано в разделе [Асинхронная интеграция микрослужб способствует их автономности](../architect-microservice-container-applications/communication-in-microservice-architecture.md#asynchronous-microservice-integration-enforces-microservices-autonomy) этого руководства.</span><span class="sxs-lookup"><span data-stu-id="c65f1-132">To minimize this problem, in the section [Asynchronous microservice integration enforce microservice’s autonomy](../architect-microservice-container-applications/communication-in-microservice-architecture.md#asynchronous-microservice-integration-enforces-microservices-autonomy), this guide encourages you to use asynchronous communication across the internal microservices.</span></span>

<span data-ttu-id="c65f1-133">Кроме того, вам необходимо разрабатывать микрослужбы и клиентские приложения с учетом возможности частичных сбоев — то есть создавать устойчивые микрослужбы и клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="c65f1-133">In addition, it's essential that you design your microservices and client applications to handle partial failures—that is, to build resilient microservices and client applications.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="c65f1-134">[Назад](index.md)
>[Вперед](partial-failure-strategies.md)</span><span class="sxs-lookup"><span data-stu-id="c65f1-134">[Previous](index.md)
[Next](partial-failure-strategies.md)</span></span>