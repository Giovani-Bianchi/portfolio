# Conventions

## Naming

| Construct | Pattern | Examples |
|-----------|---------|---------|
| Functions & variables | `camelCase` | `loadData()`, `orderTotals` |
| Interfaces | `PascalCase` + `I` prefix | `IOrder`, `IUser` |
| Types | `PascalCase` + `T` prefix | `TOrderType`, `TUserRole` |
| Enums | `PascalCase` + `Enum` suffix | `StatusEnum`, `InvoiceTypeEnum` |
| Components | `PascalCase` | `OrderCard`, `UserAvatar` |

## Folder Structure

Global utils (shared across contexts) under `/src`:

```
src/
  hooks/
  utils/
  types/      ← interfaces and types
  enums/
```

Module-local utils inside each module under `/src/app`:

```
src/app/
  orders/
    hooks/
    utils/
    types/
    enums/
  products/
    hooks/
    ...
```

Create local folders only for module-specific logic that doesn't belong globally.

## Functions

Prefer arrow functions over `function` declarations:

```ts
// Good
const formatOrder = (order: IOrder): IOrder => { ... }
const getTotal = (items: IItem[]): number => items.reduce((sum, item) => sum + item.price, 0);

// Bad
function formatOrder(order: IOrder): IOrder { ... }
function getTotal(items: IItem[]): number { ... }
```

Exception: use `function` when hoisting needed or for named module root exports (stack trace readability).

## Language

English for all code, comments, variable names, documentation.
