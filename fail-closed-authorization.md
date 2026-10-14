# Fail-Closed Authorization

**Rule:** if the system cannot work out what a user is allowed to see, it returns nothing, never everything.

## Why

Most data leaks in business apps do not come from broken login. They come from a filter that quietly disappears when something is missing: a null scope, a failed lookup, a role without configuration. "No filter" then means "all rows".

## Pattern

```ts
function scopeFilter(user): string {
  if (user.scope === 'all') return '';              // explicit full access only
  if (user.customerId)       return 'customer_id = @customerId';
  if (user.ownerCode)        return 'owner_code = @ownerCode';
  return '1 = 0';                                   // unknown -> no rows
}
```

- Full access is **granted explicitly**, never by absence.
- Every other path ends in a filter that matches nothing.
- Lookups that can fail (another service, another database) default to the **restrictive** side for reads of sensitive data.

## Checklist

- [ ] Authorization data comes from the verified token or session on the server.
- [ ] The UI hides buttons for convenience only; the API enforces everything.
- [ ] A synced or cached "flag" is never the only basis for a permission decision.
- [ ] Reports and exports use the same scope function as the screens.
- [ ] A test exists for "user with no scope sees no rows".
