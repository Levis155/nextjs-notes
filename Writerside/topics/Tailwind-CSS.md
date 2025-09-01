# Tailwind CSS

Tailwind i s a utility-first CSS framework that can be composed to build any design directly in your markup.

Some common utility classes include:

- **Paddings:** px-[number], py[number], pt-[number], pr[number] e.t.c
- **Margins:** mx-[number], my[number], ml-[number], mb[number] e.t.c
- **Text-size:** text-xs, text-sm, text-base, text-lg, text-xl, text-2xl, text-3xl, e.t.c.

**Example:**

```TSX
import AddToCart from "../AddToCart";

const ProductCard = () => {
    return(
        <div className="p-5 my-5 bg-sky-400 text-white text-xl hover:bg-sky-500">
            <AddToCart />
        </div>
    )
}

export default ProductCard;
```