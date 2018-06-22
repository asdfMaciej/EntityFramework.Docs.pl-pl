---
title: Usługi czasu projektowania — podstawowe EF
author: bricelam
ms.author: bricelam
ms.date: 10/26/2017
ms.technology: entity-framework-core
ms.openlocfilehash: f9c8208a59bfcefeaab01ea69e65fe809a0b3d89
ms.sourcegitcommit: 5e2d97e731f975cf3405ff3deab2a3c75ad1b969
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
ms.locfileid: "26054608"
---
<a name="design-time-services"></a><span data-ttu-id="45ebc-102">Usługi w czasie projektowania</span><span class="sxs-lookup"><span data-stu-id="45ebc-102">Design-time services</span></span>
====================
<span data-ttu-id="45ebc-103">Niektóre usługi używane przez narzędzia są używane tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="45ebc-103">Some services used by the tools are only used at design time.</span></span> <span data-ttu-id="45ebc-104">Te usługi są zarządzane oddzielnie od usługi czasu wykonywania EF Core, aby zapobiec wdrażany z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="45ebc-104">These services are managed separately from EF Core's runtime services to prevent them from being deployed with your app.</span></span> <span data-ttu-id="45ebc-105">Aby zastąpić jedną z tych usług (na przykład usługa generuje pliki migracji), Dodaj implementację `IDesignTimeServices` na Twój projekt startowy.</span><span class="sxs-lookup"><span data-stu-id="45ebc-105">To override one of these services (for example the service to generate migration files), add an implementation of `IDesignTimeServices` to your startup project.</span></span>

``` csharp
class MyDesignTimeServices : IDesignTimeServices
{
    public void ConfigureDesignTimeServices(IServiceCollection services)
        => services.AddSingleton<IMigrationsCodeGenerator, MyMigrationsCodeGenerator>()
}
```
