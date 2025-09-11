# Uploading to Cloudinary

To upload files to Cloudinary we'll use the CldUploadWidget imported from the next-cloudinary library.

This component is typically created in the upload/page.tsx file.

It has the uploadPreset attribute where you provide the name of your upload preset in form of a string.

Upload presets define a set of parameters to apply during uploads and are configured in the uploads section of the cloudinary platform's settings tab.

![](Screenshot (294).png) { width="450" }

**app/upload/page.tsx:**

```TSX
"use client";
import React from "react";
import { CldUploadWidget } from "next-cloudinary";

const UploadPage = () => {
  return (
    <CldUploadWidget uploadPreset="next-app-preset">
      {({ open }) => (
        <button className="btn btn-primary" onClick={() => open()}>
          Upload
        </button>
      )}
    </CldUploadWidget>
  );
};

export default UploadPage;
```