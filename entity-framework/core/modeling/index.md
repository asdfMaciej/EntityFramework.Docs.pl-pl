---
title: Tworzenie modelu — EF Core
author: rowanmiller
ms.date: 10/27/2016
ms.assetid: 88253ff3-174e-485c-b3f8-768243d01ee1
uid: core/modeling/index
ms.openlocfilehash: 67012d0f52cc77ce872fc428fccc20526f3fefad
ms.sourcegitcommit: 2b787009fd5be5627f1189ee396e708cd130e07b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45489274"
---
# <a name="creating-and-configuring-a-model"></a>Tworzenie i konfigurowanie modelu

Entity Framework używa zestawu Konwencji do zbudowania modelu oparte na kształt klas jednostek. Możesz określić dodatkowej konfiguracji w celu uzupełnienia i/lub zastąpić, co zostało wykryte przez Konwencję.

W tym artykule opisano konfiguracji, które mogą być stosowane do modelu, przeznaczone dla dowolnego magazynu danych i tych, które można zastosować w przypadku przeznaczone dla dowolnej relacyjnej bazy danych. Dostawców może też umożliwiać konfiguracji, które są specyficzne dla określonego magazynu danych. Dokumentację dotyczącą konfiguracji określonego dostawcy znaleźć [dostawcy baz danych](../providers/index.md) sekcji.

> [!TIP]  
> Można wyświetlić w tym artykule [przykładowe](https://github.com/aspnet/EntityFramework.Docs/tree/master/samples) w witrynie GitHub.

## <a name="use-fluent-api-to-configure-a-model"></a>Użyj interfejsu API fluent, aby skonfigurować model

Można zastąpić `OnModelCreating` metodę w pochodnej kontekstu i użyj `ModelBuilder API` do skonfigurowania modelu. To jest najbardziej zaawansowane metody konfiguracji i umożliwia konfigurację można określić bez konieczności wprowadzania zmian w Twoich zajęciach jednostki. Konfiguracja interfejsu API Fluent ma najwyższy priorytet i spowoduje zastąpienie danych i konwencje adnotacji.

<!-- [!code-csharp[Main](samples/core/Modeling/FluentAPI/Samples/Required.cs?range=5-15&highlight=5-10)] -->

``` csharp
    class MyContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Blog>()
                .Property(b => b.Url)
                .IsRequired();
        }
    }
```

## <a name="use-data-annotations-to-configure-a-model"></a>Umożliwia konfigurowanie modelu adnotacji danych

Atrybuty (znanych jako adnotacje danych) można zastosować także do klas i właściwości. Adnotacje danych spowoduje zastąpienie Konwencji, ale zostaną zastąpione przez interfejs Fluent API konfiguracji.

<!-- [!code-csharp[Main](samples/core/Modeling/DataAnnotations/Samples/Required.cs?range=11-16&highlight=4)] -->
``` csharp
    public class Blog
    {
        public int BlogId { get; set; }
        [Required]
        public string Url { get; set; }
    }
```
