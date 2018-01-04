# [Entity Framework](index.md)

## [Porównanie programów EF Core i EF6](efcore-and-ef6/index.md)

### [Który z nich jest odpowiedni dla Ciebie](efcore-and-ef6/choosing.md)
### [Porównanie funkcji](efcore-and-ef6/features.md)
### [Programy EF6 i EF Core w tej samej aplikacji](efcore-and-ef6/side-by-side.md)
### [Przenoszenie z programu EF6 do programu EF Core](efcore-and-ef6/porting/index.md)
#### [Sprawdzanie poprawności wymagań](efcore-and-ef6/porting/ensure-requirements.md)
#### [Przenoszenie modelu opartego na EDMX](efcore-and-ef6/porting/port-edmx.md)
#### [Przenoszenie modelu opartego na kodzie](efcore-and-ef6/porting/port-code.md)

## [Entity Framework Core](core/index.md)

### [Nowości w programie EF Core 2.0](core/what-is-new/index.md)
#### [EF Core 1.0 (poprzednia wersja)](core/what-is-new/ef-core-1.0.md)
#### [EF Core 1.1 (poprzednia wersja)](core/what-is-new/ef-core-1.1.md)

### [Wprowadzenie](core/get-started/index.md)
#### [Instalowanie programu EF Core](core/get-started/install/index.md)
#### [.NET Framework (konsola, WinForms, WPF, itd.)](core/get-started/full-dotnet/index.md)
##### [.NET Framework — nowa baza danych](core/get-started/full-dotnet/new-db.md)
##### [.NET Framework — istniejąca baza danych](core/get-started/full-dotnet/existing-db.md)
#### [.NET Core (Windows, OSX, Linux, itd.)](core/get-started/netcore/index.md)
##### [.NET Core — nowa baza danych](core/get-started/netcore/new-db-sqlite.md)
#### [ASP.NET Core](core/get-started/aspnetcore/index.md)
##### [ASP.NET Core — nowa baza danych](core/get-started/aspnetcore/new-db.md)
##### [ASP.NET Core — istniejąca baza danych](core/get-started/aspnetcore/existing-db.md)
##### [Samouczek programu EF Core w witrynie ASP.NET Core](https://docs.asp.net/en/latest/data/ef-mvc/intro.html)
#### [Platforma uniwersalna systemu Windows (UWP)](core/get-started/uwp/index.md)
##### [Platforma UWP — nowa baza danych](core/get-started/uwp/getting-started.md)

### [Tworzenie modelu](core/modeling/index.md)
#### [Uwzględnianie i wykluczanie typów](core/modeling/included-types.md)
#### [Uwzględnianie i wykluczanie właściwości](core/modeling/included-properties.md)
#### [Klucze (podstawowe)](core/modeling/keys.md)
#### [Generowane wartości](core/modeling/generated-properties.md)
#### [Właściwości wymagane/opcjonalne](core/modeling/required-optional.md)
#### [Maksymalna długość](core/modeling/max-length.md)
#### [Tokeny współbieżności](core/modeling/concurrency.md)
#### [Właściwości w tle](core/modeling/shadow-properties.md)
#### [Relacje](core/modeling/relationships.md)
#### [Indeksy](core/modeling/indexes.md)
#### [Klucze alternatywne](core/modeling/alternate-keys.md)
#### [Dziedziczenie](core/modeling/inheritance.md)
#### [Pola zapasowe](core/modeling/backing-field.md)
#### [Modele naprzemienne z tym samym typem DbContext](core/modeling/dynamic-model.md)
#### [Modelowanie relacyjnej bazy danych](core/modeling/relational/index.md)
##### [Mapowanie tabeli](core/modeling/relational/tables.md)
##### [Mapowanie kolumn](core/modeling/relational/columns.md)
##### [Typy danych](core/modeling/relational/data-types.md)
##### [Klucze podstawowe](core/modeling/relational/primary-keys.md)
##### [Schemat domyślny](core/modeling/relational/default-schema.md)
##### [Kolumny obliczane](core/modeling/relational/computed-columns.md)
##### [Sekwencje](core/modeling/relational/sequences.md)
##### [Wartości domyślne](core/modeling/relational/default-values.md)
##### [Indeksy](core/modeling/relational/indexes.md)
##### [Ograniczenia klucza obcego](core/modeling/relational/fk-constraints.md)
##### [Klucze alternatywne (ograniczenia unikatowe)](core/modeling/relational/unique-constraints.md)
##### [Dziedziczenie (relacyjna baza danych)](core/modeling/relational/inheritance.md)

### [Wykonanie zapytania o dane](core/querying/index.md)
#### [Zapytanie podstawowe](core/querying/basic.md)
#### [Ładowanie powiązanych danych](core/querying/related-data.md)
#### [Klient a wyznaczenie wartości na serwerze](core/querying/client-eval.md)
#### [Śledzenie a brak śledzenia](core/querying/tracking.md)
#### [Pierwotne zapytania SQL](core/querying/raw-sql.md)
#### [Zapytania asynchroniczne](core/querying/async.md)
#### [Jak działa zapytanie](core/querying/overview.md)
#### [Filtry zapytań globalnych](core/querying/filters.md)

### [Zapisywanie danych](core/saving/index.md)
#### [Zapisywanie podstawowe](core/saving/basic.md)
#### [Powiązane dane](core/saving/related-data.md)
#### [Usuwanie kaskadowe](core/saving/cascade-delete.md)
#### [Konflikty współbieżności](core/saving/concurrency.md)
#### [Transakcje](core/saving/transactions.md)
#### [Zapisywanie asynchroniczne](core/saving/async.md)
#### [Odłączone jednostki](core/saving/disconnected-entities.md)
#### [Jawne wartości dla wygenerowanych właściwości](core/saving/explicit-values-generated-properties.md)

### [Obsługiwane implementacje platformy .NET](core/platforms/index.md)

### [Dostawcy baz danych](core/providers/index.md)
#### [Microsoft SQL Server](core/providers/sql-server/index.md)
##### [Tabele zoptymalizowane pod kątem pamięci](core/providers/sql-server/memory-optimized-tables.md)
#### [SQLite](core/providers/sqlite/index.md)
##### [Ograniczenia SQLite](core/providers/sqlite/limitations.md)
#### [PostgreSQL (Npgsql)](core/providers/npgsql/index.md)
#### [IBM Data Server (DB2)](core/providers/ibm/index.md)
#### [MySQL (Official)](core/providers/mysql/index.md)
#### [MySQL (Pomelo)](core/providers/pomelo/index.md)
#### [Microsoft SQL Server Compact Edition](core/providers/sql-compact/index.md)
#### [InMemory (do testowania)](core/providers/in-memory/index.md)
#### [Devart (m.in. MySQL, Oracle, PostgreSQL, SQLite, DB2)](core/providers/devart/index.md)
#### [Oracle (jeszcze niedostępny)](core/providers/oracle/index.md)
#### [MyCat](core/providers/my-cat/index.md)
#### [Firebird-Community](core/providers/firebird-community/index.md)
#### [Tworzenie dostawcy bazy danych](core/providers/writing-a-provider.md)

### [Zarządzanie schematami bazy danych](core/managing-schemas/index.md)
#### [Migracje](core/managing-schemas/migrations/index.md)
##### [Środowiska zespołowe](core/managing-schemas/migrations/teams.md)
##### [Operacje niestandardowe](core/managing-schemas/migrations/operations.md)
##### [Korzystanie z osobnego projektu](core/managing-schemas/migrations/projects.md)
##### [Wielu dostawców](core/managing-schemas/migrations/providers.md)
##### [Niestandardowa tabela historii](core/managing-schemas/migrations/history-table.md)
#### [🔧 Tworzenie i upuszczanie interfejsów API](core/managing-schemas/ensure-created.md)
#### [🔧 Odtwarzanie](core/managing-schemas/scaffolding.md)

### [Dokumentacja wiersza polecenia](core/miscellaneous/cli/index.md)
#### [Konsola menedżera pakietów (Visual Studio)](core/miscellaneous/cli/powershell.md)
#### [.NET Core CLI](core/miscellaneous/cli/dotnet.md)
#### [Tworzenie typu DbContext w czasie projektowania](core/miscellaneous/cli/dbcontext-creation.md)
#### [Usługi w czasie projektowania](core/miscellaneous/cli/services.md)

### [Narzędzia i rozszerzenia](core/extensions/index.md)
#### [LLBLGen Pro](core/extensions/llbl-gen-pro.md)
#### [Devart Entity Developer](core/extensions/devart-entity-developer.md)
#### [EFSecondLevelCache.Core](core/extensions/efsecondlevelcache-core.md)
#### [Geco (generator modelu odwróconego)](core/extensions/geco.md)
#### [EntityFrameworkCore.Detached](core/extensions/entityframeworkcore-detached.md)
#### [EntityFrameworkCore.Triggers](core/extensions/entityframeworkcore-triggers.md)
#### [EntityFrameworkCore.Rx](core/extensions/entityframeworkcore-rx.md)
#### [EntityFrameworkCore.PrimaryKey](core/extensions/entityframeworkcore-primarykey.md)
#### [EntityFrameworkCore.TypedOriginalValues](core/extensions/entityframeworkcore-typedoriginalvalues.md)
#### [EFCore.Practices](core/extensions/efcore-practices.md)
#### [LinqKit.Microsoft.EntityFrameworkCore](core/extensions/linqkit.md)
#### [Microsoft.EntityFrameworkCore.AutoHistory](core/extensions/autohistory.md)
#### [Microsoft.EntityFrameworkCore.DynamicLinq](core/extensions/dynamiclinq.md)
#### [Microsoft.EntityFrameworkCore.UnitOfWork](core/extensions/unitofwork.md)

### Różne
#### [Parametry połączeń](core/miscellaneous/connection-strings.md)
#### [Rejestrowanie](core/miscellaneous/logging.md)
#### [Elastyczność połączenia](core/miscellaneous/connection-resiliency.md)
#### [Testowanie](core/miscellaneous/testing/index.md)
##### [Testowanie za pomocą SQLite](core/miscellaneous/testing/sqlite.md)
##### [Testowanie za pomocą InMemory](core/miscellaneous/testing/in-memory.md)
#### [Konfigurowanie typu DbContext](core/miscellaneous/configuring-dbcontext.md)
#### [Uaktualnienie z wersji 1.0 RC1 do RC2](core/miscellaneous/rc1-rc2-upgrade.md)
#### [Uaktualnienie z wersji 1.0 RC2 do RTM](core/miscellaneous/rc2-rtm-upgrade.md)
#### [Uaktualnianie do EF Core 2.0](core/miscellaneous/1x-2x-upgrade.md)

### [⤤ Dokumentacja interfejsu API](https://docs.microsoft.com/dotnet/api/?view=efcore-2.0)

## [Entity Framework 6](ef6/index.md)
### [⤤ Dokumentacja](http://msdn.com/data/ef)
### [⤤ Dokumentacja interfejsu API](https://msdn.microsoft.com/library/dn223258.aspx)