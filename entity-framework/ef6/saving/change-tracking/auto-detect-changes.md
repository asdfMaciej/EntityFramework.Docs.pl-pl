---
title: Automatyczne wykrywanie zmian — EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: a8d1488d-9a54-4623-a76b-e81329ff2756
caps.latest.revision: 3
ms.openlocfilehash: 62f2f026426346fc1230a2f5743c8cb7d232ec7f
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2018
ms.locfileid: "37912002"
---
# <a name="automatic-detect-changes"></a><span data-ttu-id="7e7de-102">Automatyczne wykrywanie zmian</span><span class="sxs-lookup"><span data-stu-id="7e7de-102">Automatic detect changes</span></span>
<span data-ttu-id="7e7de-103">Korzystając z większości obiektów POCO ustalenia, jak jednostki został zmieniony (i w związku z tym aktualizacje, które muszą być wysyłane do bazy danych) odbywa się przez algorytm wykrywa zmiany.</span><span class="sxs-lookup"><span data-stu-id="7e7de-103">When using most POCO entities the determination of how an entity has changed (and therefore which updates need to be sent to the database) is handled by the Detect Changes algorithm.</span></span> <span data-ttu-id="7e7de-104">Wykryj zmiany działa został określony poprzez wykrycie różnic między bieżącej wartości właściwości jednostki i oryginalne wartości właściwości, które są przechowywane w migawce jednostki zapytania lub został dołączony.</span><span class="sxs-lookup"><span data-stu-id="7e7de-104">Detect Changes works by detecting the differences between the current property values of the entity and the original property values that are stored in a snapshot when the entity was queried or attached.</span></span> <span data-ttu-id="7e7de-105">Techniki przedstawione w tym temacie stosuje się jednakowo do modeli utworzonych za pomocą Code First i projektancie platformy EF.</span><span class="sxs-lookup"><span data-stu-id="7e7de-105">The techniques shown in this topic apply equally to models created with Code First and the EF Designer.</span></span>  

<span data-ttu-id="7e7de-106">Domyślnie program Entity Framework wykonuje wykrywać zmiany automatycznie wywołanego następujących metod:</span><span class="sxs-lookup"><span data-stu-id="7e7de-106">By default, Entity Framework performs Detect Changes automatically when the following methods are called:</span></span>  

- <span data-ttu-id="7e7de-107">DbSet.Find</span><span class="sxs-lookup"><span data-stu-id="7e7de-107">DbSet.Find</span></span>  
- <span data-ttu-id="7e7de-108">DbSet.Local</span><span class="sxs-lookup"><span data-stu-id="7e7de-108">DbSet.Local</span></span>  
- <span data-ttu-id="7e7de-109">DbSet.Add</span><span class="sxs-lookup"><span data-stu-id="7e7de-109">DbSet.Add</span></span>  
- <span data-ttu-id="7e7de-110">DbSet.AddRange</span><span class="sxs-lookup"><span data-stu-id="7e7de-110">DbSet.AddRange</span></span>
- <span data-ttu-id="7e7de-111">DbSet.Remove</span><span class="sxs-lookup"><span data-stu-id="7e7de-111">DbSet.Remove</span></span>  
- <span data-ttu-id="7e7de-112">DbSet.RemoveRange</span><span class="sxs-lookup"><span data-stu-id="7e7de-112">DbSet.RemoveRange</span></span>
- <span data-ttu-id="7e7de-113">DbSet.Attach</span><span class="sxs-lookup"><span data-stu-id="7e7de-113">DbSet.Attach</span></span>  
- <span data-ttu-id="7e7de-114">DbContext.SaveChanges</span><span class="sxs-lookup"><span data-stu-id="7e7de-114">DbContext.SaveChanges</span></span>  
- <span data-ttu-id="7e7de-115">DbContext.GetValidationErrors</span><span class="sxs-lookup"><span data-stu-id="7e7de-115">DbContext.GetValidationErrors</span></span>  
- <span data-ttu-id="7e7de-116">DbContext.Entry</span><span class="sxs-lookup"><span data-stu-id="7e7de-116">DbContext.Entry</span></span>  
- <span data-ttu-id="7e7de-117">DbChangeTracker.Entries</span><span class="sxs-lookup"><span data-stu-id="7e7de-117">DbChangeTracker.Entries</span></span>  

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="7e7de-118">Wyłączenie automatycznego wykrywania zmian</span><span class="sxs-lookup"><span data-stu-id="7e7de-118">Disabling automatic detection of changes</span></span>  

<span data-ttu-id="7e7de-119">Jeśli śledzisz partii jednostek w kontekst można wywołać jedną z następujących metod wiele razy w pętli, może zostać znaczne ulepszenia wydajności przez wyłączenie wykrywania zmian na czas trwania pętli.</span><span class="sxs-lookup"><span data-stu-id="7e7de-119">If you are tracking a lot of entities in your context and you call one of these methods many times in a loop, then you may get significant performance improvements by turning off detection of changes for the duration of the loop.</span></span> <span data-ttu-id="7e7de-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7e7de-120">For example:</span></span>  

``` csharp
using (var context = new BloggingContext())
{
    try
    {
        context.Configuration.AutoDetectChangesEnabled = false;

        // Make many calls in a loop
        foreach (var blog in aLotOfBlogs)
        {
            context.Blogs.Add(blog);
        }
    }
    finally
    {
        context.Configuration.AutoDetectChangesEnabled = true;
    }
}
```  

<span data-ttu-id="7e7de-121">Nie należy zapominać ponownie włączyć funkcję wykrywania zmian po pętli — używaliśmy try/finally aby upewnić się, nawet wtedy, gdy kod w pętli zgłasza wyjątek zawsze jest ponownie włączone.</span><span class="sxs-lookup"><span data-stu-id="7e7de-121">Don’t forget to re-enable detection of changes after the loop — We've used a try/finally to ensure it is always re-enabled even if code in the loop throws an exception.</span></span>  

<span data-ttu-id="7e7de-122">Alternatywa wyłączenie i ponowne włączenie pozostaw automatyczne wykrywanie zmian wyłączony na cały czas i albo Kontekst wywołania. ChangeTracker.DetectChanges jawnie lub użyj zmienić przerwami proxy śledzenia.</span><span class="sxs-lookup"><span data-stu-id="7e7de-122">An alternative to disabling and re-enabling is to leave automatic detection of changes turned off at all times and either call context.ChangeTracker.DetectChanges explicitly or use change tracking proxies diligently.</span></span> <span data-ttu-id="7e7de-123">Obie te opcje są zaawansowane i łatwo wprowadzić drobne błędy do aplikacji więc używane ostrożnie.</span><span class="sxs-lookup"><span data-stu-id="7e7de-123">Both of these options are advanced and can easily introduce subtle bugs into your application so use them with care.</span></span>  

<span data-ttu-id="7e7de-124">Jeśli potrzebujesz dodać lub usunąć wiele obiektów z kontekstu, należy wziąć pod uwagę przy użyciu DbSet.AddRange i DbSet.RemoveRange.</span><span class="sxs-lookup"><span data-stu-id="7e7de-124">If you need to add or remove many objects from a context, consider using DbSet.AddRange and DbSet.RemoveRange.</span></span> <span data-ttu-id="7e7de-125">Ta metoda automatycznie Wykryj zmiany tylko jeden raz po ukończeniu operacji dodawania lub usuwania.</span><span class="sxs-lookup"><span data-stu-id="7e7de-125">This methods automatically detect changes only once after the add or remove operations are completed.</span></span> 