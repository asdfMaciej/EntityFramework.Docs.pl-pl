---
title: Mapowanie kolumny - EF Core
author: rowanmiller
ms.author: divega
ms.date: 10/27/2016
ms.assetid: 05a47de9-1078-488e-a823-b516a4208f33
ms.technology: entity-framework-core
uid: core/modeling/relational/columns
ms.openlocfilehash: 697b966dbac892e332fe65feaa4dd11f00dd8298
ms.sourcegitcommit: 01a75cd483c1943ddd6f82af971f07abde20912e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2017
---
# <a name="column-mapping"></a><span data-ttu-id="f49e6-102">Mapowanie kolumny</span><span class="sxs-lookup"><span data-stu-id="f49e6-102">Column Mapping</span></span>

> [!NOTE]  
> <span data-ttu-id="f49e6-103">Konfiguracja opisana w tej sekcji ma zastosowanie do relacyjnych baz danych w zasadzie.</span><span class="sxs-lookup"><span data-stu-id="f49e6-103">The configuration in this section is applicable to relational databases in general.</span></span> <span data-ttu-id="f49e6-104">Metody rozszerzenia pokazane staną się dostępne po zainstalowaniu dostawcy relacyjnej bazy danych (z powodu udostępnionego *Microsoft.EntityFrameworkCore.Relational* pakietu).</span><span class="sxs-lookup"><span data-stu-id="f49e6-104">The extension methods shown here will become available when you install a relational database provider (due to the shared *Microsoft.EntityFrameworkCore.Relational* package).</span></span>

<span data-ttu-id="f49e6-105">Mapowanie kolumny określa dane, które kolumny powinny być pobierane z i zapisane w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f49e6-105">Column mapping identifies which column data should be queried from and saved to in the database.</span></span>

## <a name="conventions"></a><span data-ttu-id="f49e6-106">Konwencje</span><span class="sxs-lookup"><span data-stu-id="f49e6-106">Conventions</span></span>

<span data-ttu-id="f49e6-107">Konwencja każda właściwość będzie Instalatora, aby mapować do kolumny o takiej samej nazwie jak właściwość.</span><span class="sxs-lookup"><span data-stu-id="f49e6-107">By convention, each property will be setup to map to a column with the same name as the property.</span></span>

## <a name="data-annotations"></a><span data-ttu-id="f49e6-108">Adnotacji danych</span><span class="sxs-lookup"><span data-stu-id="f49e6-108">Data Annotations</span></span>

<span data-ttu-id="f49e6-109">Adnotacje danych służy do konfigurowania kolumn, z którą właściwość jest zamapowana.</span><span class="sxs-lookup"><span data-stu-id="f49e6-109">You can use Data Annotations to configure the column to which a property is mapped.</span></span>

<!-- [!code-csharp[Main](samples/core/relational/Modeling/DataAnnotations/Samples/Relational/Column.cs?highlight=3)] -->
``` csharp
public class Blog
{
    [Column("blog_id")]
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

## <a name="fluent-api"></a><span data-ttu-id="f49e6-110">Interfejsu API Fluent</span><span class="sxs-lookup"><span data-stu-id="f49e6-110">Fluent API</span></span>

<span data-ttu-id="f49e6-111">Interfejsu API Fluent służy do konfigurowania kolumn, z którą właściwość jest zamapowana.</span><span class="sxs-lookup"><span data-stu-id="f49e6-111">You can use the Fluent API to configure the column to which a property is mapped.</span></span>

<!-- [!code-csharp[Main](samples/core/relational/Modeling/FluentAPI/Samples/Relational/Column.cs?highlight=7,8,9)] -->
``` csharp
class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Blog>()
            .Property(b => b.BlogId)
            .HasColumnName("blog_id");
    }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```
