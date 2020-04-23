---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: c3746ff92838ac97d8158a0daf0b1a1de07ae024
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2020
ms.locfileid: "81433220"
---
<span data-ttu-id="077e8-101">Чтобы использовать библиотеки управления Azure для .NET, приложению .NET требуются разрешения на чтение и создание ресурсов в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="077e8-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="077e8-102">Создайте субъект-службу и настройте приложение для выполнения с ее учетными данными, чтобы предоставить ему такие права доступа.</span><span class="sxs-lookup"><span data-stu-id="077e8-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="077e8-103">Субъект-служба помогает создать неинтерактивную учетную запись, связанную с вашим идентификатором. Этой учетной записи предоставляются только разрешения, необходимые для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="077e8-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="077e8-104">Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="077e8-104">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="077e8-105">Убедитесь, что вы используете подписку, в которой будет создан субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="077e8-105">Verify you are currently using the subscription in which you want the service principal created.</span></span>

```azurecli-interactive
az account show
```

<span data-ttu-id="077e8-106">Сведения о подписке отображаются.</span><span class="sxs-lookup"><span data-stu-id="077e8-106">Your subscription information is displayed.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

<span data-ttu-id="077e8-107">Если вы вошли в неправильную подписку, введите `az account set -s <name or ID of subscription>`, чтобы выбрать правильную.</span><span class="sxs-lookup"><span data-stu-id="077e8-107">If you're not logged into the correct subscription, select the correct one by typing `az account set -s <name or ID of subscription>`.</span></span>

<span data-ttu-id="077e8-108">Создайте субъект-службу с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="077e8-108">Create the service principal with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

<span data-ttu-id="077e8-109">Сведения о субъекте-службе отображаются в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="077e8-109">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="077e8-110">Скопируйте и вставьте выходные данные JSON в текстовый редактор для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="077e8-110">Copy and paste the JSON output to a text editor for use later.</span></span>