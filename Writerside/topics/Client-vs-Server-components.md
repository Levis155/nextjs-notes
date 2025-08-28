# Client vs Server components

## Rendering Environments

In Next.js projects we have 2 environments where we can render our components and generate html markup:
- CSR (Client-side Rendering) - In the client within a web browser 
- SSR (Server-side Rendering) - On the server within a Node.js Runtime.

### CSR vs SSR Features

<table>
    <tr>
        <th>Client-side Rendering</th>
        <th>Server-side Rendering</th>
    </tr>
    <tr>
        <td>Large bundles</td>
        <td>Smaller bundles</td>
    </tr>
    <tr>
        <td>Resource intensive</td>
        <td>Resource efficient</td>
    </tr>
    <tr>
        <td>No SEO</td>
        <td>SEO</td>
    </tr>
    <tr>
        <td>Less secure</td>
        <td>More secure</td>
    </tr>
</table>

Despite having all these great benefits, server components do not have interactivity thus they cannot:
- Listen to browser events
- Access browser APIs
- Maintain state
- Use effects

> In real-world applications a mixture of both client-side and server-side applications are used. It is best practice to default to server-side components and use client-side components when they are absolutely needed.

### Mixing CSR and SSR components

Say for instance you're building a page to show a list of products. To build this page you probably need a productCard component.

To add a product to a shopping cart you'll need to handle the click event of a button in the product card. To implement this we can:

- Make the whole component a client-component using the `use client` directive.

```tsx
'use client';

const ProductCard = () => {
    return(
        <div>
            <button onClick={() => console.log("Click!")}>Add to Cart</button>
        </div>
    )
}

export default ProductCard;
 ```

- Keep the component in the server and do most of the rendering there and extract only a small component that contains the add button. **(This is the recommended way as most of the rendering is done on the server thus ultimately improving the speed of your application.)**

**AddToCart component:**
```tsx
'use client';

const AddToCart = () => {
  return (
    <div>
      <button onClick={() => console.log("Click!")}>Add to Cart</button>
    </div>
  )
}

export default AddToCart

```
**ProductCard component:**

```tsx
import AddToCart from "./AddToCart";

const ProductCard = () => {
    return(
        <div>
            <AddToCart />
        </div>
    )
}

export default ProductCard;
```