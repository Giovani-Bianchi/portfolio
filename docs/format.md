# Code Format

## Section grouping

Group related blocks with section comment using `--` delimiters:

```tsx
// -- Hooks --

const router = useRouter();
const pathname = usePathname();

// -- States --

const [isLoading, setIsLoading] = useState<boolean>(false);
const [order, setOrder] = useState<IOrder>(initialOrder);
```

Common labels: `Hooks`, `States`, `Effects`, `Helpers`, `Handlers`, `Constants`, `[Context] Constants` (e.g. `Order Constants`).

## JSDoc on functions

Document every non-trivial function with description, params, return, example:

```ts
/**
 * Formats a list of orders for display.
 * @param orders Array of raw orders to format
 * @returns Array of formatted orders
 * @example
 * const formatted = formatOrders(rawOrders);
 */
const formatOrders = (orders: IOrder[]): IOrder[] => { ... }
```

## Line spacing

Blank line between unrelated statements, even within same block:

```ts
const order = getOrderById(orderId);
const formattedOrder = formatOrder(order);

const product = getProductById(productId);
```

Spacing signals context shifts — not only different domains, but whenever next line starts new logical step.

## Blank line before `return`

Always blank line before `return`:

```ts
const formatOrder = (order: IOrder) => {
  const formattedType = FormattedOrderTypeEnum[order.type];

  return {
    ...order,
    type: formattedType,
  };
};
```

## Iteration variable names

Full names in iteration callbacks. No 1–3 char abbreviations:

```ts
// Good
const orderIds = orders.map((order) => order._id);

// Bad
const orderIds = orders.map((o) => o._id);
const orderIds = orders.map((ord) => ord._id);
```

Check name collisions with outer-scope variables before choosing iteration name.