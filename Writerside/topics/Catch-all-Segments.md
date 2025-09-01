# Catch-all Segments

Sometimes we need a varying number of parameters in a route. For instance, you might want to build a page to show products the following could be possible routes:

- `/products` → To view all products
- `/products/grocery` → To view grocery products
- `/products/grocery/dairy` → To view dairy products under groceries
- `/products/grocery/dairy/milk` → To view milk products under dairy.

To implement this create a new folder `[[...slug]]/` in the directory `app/products/`

> The slug folder is prefixed with `...` to allow it to accept a varying number of parameters. It is wrapped with double square brackets to make the slug parameter optional.

To access the route parameters we need to pass props to the component being returned as follows:

**app/products/[[...slug]]/page.tsx:**

```TSX
import React from 'react'

interface Props {
    params : {slug: string[]}
}

const ProductPage = ({params: {slug}}: Props) => {
  return (
    <div>
      ProductPage {slug}
    </div>
  )
}

export default ProductPage

```