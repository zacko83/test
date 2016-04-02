# Coding Conventions

## C# Styling and Naming

Most styling and naming conventions are enforced by [StyleCop](DevTools.md). So we only consider the exceptions here:

- **Comments**: Strict rules for enforcing comments of classes, methods and properties will only lead to automatically generated comments (e.g. via GhostDoc). Therefore we decided to disable all documentation rules of StyleCop. So there is no obligation to comment each and every line of code.
- **Prefixes**: Private fields must begin with a underscore (e.g. `_localField`) instead of prefixing all local calls with `this.`.
- **Tabs vs. Spaces**: For code indention we use tabs instead of spaces (make sure your [Visual Studio](DevTools.md) is configured correctly).
- **Constants**: The names of constants must be written in upper case. Underscores may be used for readability (e.g. `MAXIMUM_NUMBER_OF_PERSONS`).
- **Using Directives**: Two of the rules for placing using directives seemed to be too strict without providing any benefit. Therefore we disabled rule SA1200 and SA1208.

## [CSS/SASS](CssRules.md)

## JavaScript

TBD

## SQL

### Formatting Rules

- Each part of a statement must be indented by a tab.
- For table abbreviations combine the capitals of a tables' name (e.g. `HotelMaster` –> `HM`).
- All key words must be written in upper case.
- All column names must be put in square brackets (e.g. `[Id]`).
- All objects must be prefixed with the schema (e.g. `dbo.`).
- When writing `WHERE`-Clauses, the logical operator must be placed at the end of the line. For short statements it's allowed to put the operator between the conditions on one line.
- Parameters of a stored procedure are written in pascal case (e.g. `@VeryNiceParameter`)
- Each parameter of a stored procedure has to be placed in a separate line.
- If a parameter of a stored procedure is passed to dynamic SQL, the parameter must be prefixed with `Param` (e.g. `@HotelMasterId` > `@HotelMasterIdParam`).

Example of a well formatted SP:

```sql
CREATE PROCEDURE [dbo].[TS_CRSTaxInformation_GetProperties_NoLock]
    @HotelMasterId INT
AS
    SELECT
        HHM.[HotelMasterId]
    FROM
        dbo.CRSTaxInformation CTI WITH (NOLOCK)
    INNER JOIN
        dbo.HT_HotelMaster HHM WITH (NOLOCK) ON HHT.[HotelMasterId] = CTI.[HotelMasterId]
    WHERE
        CTI.[HotelMasterId] = @HotelMasterId AND
        (CTI.[HotelMaster] = 1 OR CTI.[HotelMaster] > 1000) AND
        (
            (CTI.[HotelMaster] = 2 AND CTI.[HotelMaster] < 10) OR
            (CTI.[HotelMaster] = 2000 AND CTI.[HotelMaster] < 2010)
        )
GO
```

### Performance Rules

- `TEXT` and `NTEXT` are obsolete, use `VARCHAR(MAX)` and `NVARCHAR(MAX)`.
- Only use the N-datatypes only when unicode is really needed.
- Always use `WITH(NOLOCK)` when accessing tables. Exceptions from this rule have to be discussed with team performance.
- Avoid `ORDER BY` and `DISTINCT`. Filtering and ordering should be done on application level. Exceptions from this rule have to be discussed with team performance.
- For all changes to a stored procedure, the execution plan of the old and the new procedure have to be compared and optimized.
- Statements in the `WHERE` clause like `@Parameter IS NULL OR Table.Column = @Parameter` must be avoided. Use dynamic SQL instead.
- Functions on columns must be avoided.
- CTEs (Common Table Expressions) improve readability.
- For dynamic SQL `sp_executesql` must be used.
- `SET NOCOUNT ON` must be put at the beginning of each stored procedure.
- Avoid the use of th `IN` statement, as it's taking `NULL` values into account and returns a list of values. Use `EXISTS` instead, it only returns `TRUE` or `FALSE`.
- `SELECT * FROM XXX` must only be used, if really all columns shell be selected.

## English Only

No matter which programming or markup language we are talking about, the only natural language we use for coding is English. This counts not only for the code itself (variables, classes, comments etc.), but also for file names, tables and databases. Even when you write a documentation, English is the language of choice.
