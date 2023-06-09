# npm-playground
A playground to help demonstrate how deps work

- A (app)
- R (react)
- D (design system)
- M (mui)
- X (x-date-pickers)

- everyone depends on react:
  - A has dependency on R
  - D has peer dependency on R
  - M has peer dependency on R
  - X has peer dependency on R
- app depends on design system, mui:
  - A has dependency on D
  - A has dependency on M
- design system depends on mui and x-date-pickers:
  - D has peer dependency on M
  - D has dependency on X


## Outcome

A ends up with three copies of R, each scoped to their owner:

```
package-a/node_modules/package-d
package-a/node_modules/package-d/node_modules/package-m
package-a/node_modules/package-d/node_modules/package-m/node_modules/package-r   (!)
package-a/node_modules/package-d/node_modules/package-r                          (!)
package-a/node_modules/package-d/node_modules/package-x
package-a/node_modules/package-d/node_modules/package-x/node_modules/package-r   (!)
package-a/node_modules/package-m/...
package-a/node_modules/package-r                                                 (!)
```

- because A does not directly depend on X, A's node_modules does not contain X
  - but since D does directly depend on X, D's node_modules within A's node_modules does contain X