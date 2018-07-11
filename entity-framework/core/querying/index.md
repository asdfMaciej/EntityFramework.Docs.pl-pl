---
title: Wykonywanie zapytania o dane — EF Core
author: rowanmiller
ms.author: divega
ms.date: 10/27/2016
ms.assetid: 7c65ec3e-46c8-48f8-8232-9e31f96c277b
ms.technology: entity-framework-core
uid: core/querying/index
ms.openlocfilehash: 447f48b780bc48b7a79153d17dcc1b8ef0cc508c
ms.sourcegitcommit: bdd06c9a591ba5e6d6a3ec046c80de98f598f3f3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2018
ms.locfileid: "37949278"
---
# <a name="querying-data"></a><span data-ttu-id="05d39-102">Wykonanie zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="05d39-102">Querying Data</span></span>

<span data-ttu-id="05d39-103">Entity Framework Core używa Language Integrated Query (LINQ) do zapytania o dane z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="05d39-103">Entity Framework Core uses Language Integrated Query (LINQ) to query data from the database.</span></span> <span data-ttu-id="05d39-104">LINQ umożliwia przy użyciu języka C# (lub wybranym języku .NET) do pisania zapytań silnie typizowaną oparte na klasach pochodnych kontekstu i jednostki.</span><span class="sxs-lookup"><span data-stu-id="05d39-104">LINQ allows you to use C# (or your .NET language of choice) to write strongly typed queries based on your derived context and entity classes.</span></span> <span data-ttu-id="05d39-105">Reprezentacja zapytania LINQ są przekazywane do dostawcy bazy danych, aby być przetłumaczony na język zapytań specyficznych dla bazy danych (na przykład SQL dla relacyjnej bazy danych).</span><span class="sxs-lookup"><span data-stu-id="05d39-105">A representation of the LINQ query is passed to the database provider, to be translated in database-specific query language (for example, SQL for a relational database).</span></span> <span data-ttu-id="05d39-106">Aby uzyskać bardziej szczegółowe informacje dotyczące sposobu przetwarzania zapytania, zobacz [jak działa zapytanie](overview.md).</span><span class="sxs-lookup"><span data-stu-id="05d39-106">For more detailed information on how a query is processed, see [How Query Works](overview.md).</span></span>
