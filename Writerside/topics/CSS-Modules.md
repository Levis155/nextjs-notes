# CSS Modules

A CSS module is a file that is scoped to a page or a component.

It is a way to prevent styles from clashing or overwriting each other. 

> Class-clashing is avoided by employing the postcss.config.js tool which auto-generates css classes and replaces the custom classes we've assigned with these auto-generated ones

For instance, we can have a ProductCard component using styles from a **ProductCard.module.css** file. It is important to note that this file should have the **module.css** extension.

We can define classes in this css module and then import the stylesheet in the component. Typically the name styles is assigned when importing and this becomes a JavaScript object with the classes defined in the css module as the properties of the object.

This means the classes should use a camel-case naming convention i.e. **a class `card-container` would be invalid but `cardContainer` would be valid.**

**ProductCard.module.css:**

```css
.cardContainer {
    border: 1px solid red;
    padding: 1rem;
}
```

**ProductCard.tsx:**

```tsx
import AddToCart from "../AddToCart";
import styles from "./ProductCard.module.css"

const ProductCard = () => {
    return(
        <div className={styles.cardContainer}>
            <AddToCart />
        </div>
    )
}

export default ProductCard;
```