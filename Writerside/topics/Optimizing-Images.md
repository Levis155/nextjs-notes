# Optimizing Images

Next.js offers an Image component that is defined in the `next/image` package. This component is built on top of the standard image element in html but under the hood it automatically compresses and resizes our images based on the device size.

It is always recommended to use this image component in Next.js applications as opposed to the standard image element in html. 

To use this component, we have to set a number of props.

We can set the `src` prop to a file that we statically import at the top and this is useful to images that are local to our application e.g. logos, backgrounds e.t.c.

```TSX
import Image from "next/image";
import deadpool from '@/public/images/wallpaperflare.com_wallpaper 7.jpg'

export default async function Home() {

  return (
    <main>
      <Image src={deadpool} alt="deadpool" />
    </main>
  )
}

```

For remote images we have to register the domain of the string passed in `src` in the `next.config.js` file as shown:

```JS
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "bit.ly",
      },
    ],
  },
};

module.exports = nextConfig;

```

Then set src to the url of the image:

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        width={300}
        height={170}
      />
    </main>
  );
}
```

With remote images you should always provide the dimensions because Next.js doesn't know their size ahead of time.

If you want to make your images responsive so they look great on all device sizes instead of width and size you should set **fill**

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
      />
    </main>
  );
}
```

To maintain the image's aspect ratio you could either set style to an object as shown:

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
        style={{objectFit: 'cover'}}
      />
    </main>
  );
}

```

Or you could use Tailwind:

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
        className="object-cover"
      />
    </main>
  );
}
```

When showing responsive images using the `fill` prop, we often need to set `sizes` as well and this determines how much of the width of the viewport the image takes.

For instance say we want to render a page like Instagram i.e. single column on mobile, two columns on mobile, and 3 columns on desktops: 

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
        className="object-cover"
        sizes="(max-width: 480px) 100vw, (max-width: 768px) 50vw, 33vw"
      />
    </main>
  );
}
```

Another prop you can set is `quality` which by default is 75. You can set this to 100 for background images.

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
        className="object-cover"
        sizes="(max-width: 480px) 100vw, (max-width: 768px) 50vw, 33vw"
        quality={100}
      />
    </main>
  );
}
```

We also have `priority` prop which is a boolean and is set for images which should appear above the viewport.

```TSX
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt="react cover"
        fill
        className="object-cover"
        sizes="(max-width: 480px) 100vw, (max-width: 768px) 50vw, 33vw"
        quality={100}
        priority
      />
    </main>
  );
}

```