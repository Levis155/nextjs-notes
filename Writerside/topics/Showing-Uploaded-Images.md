# Showing Uploaded Images

The CldUploadWidget component has an onSuccess event that gets triggered everytime a file is uploaded successfully.

We pass a function to the onSuccess attribute that takes a result object as on of its parameters. This object has the image's publicId as one of its properties.

We can use the cldImage component to show the image uploaded setting the src to the image's publicId as shown:

```TSX
"use client";
import React, { useState } from "react";
import { CldImage, CldUploadWidget } from "next-cloudinary";

interface CloudinaryResult {
  public_id: string;
}

const UploadPage = () => {
  const [publicId, setPublicId] = useState("");

  return (
    <>
      {publicId && (
        <CldImage src={publicId} alt="A happy dog" width={270} height={180} />
      )}
      <CldUploadWidget
        uploadPreset="next-app-preset"
        onSuccess={(result, { widget }) => {
          const info = result?.info as CloudinaryResult;
          if (info?.public_id) {
            setPublicId(info.public_id);
            widget.close(); // Optionally close the widget after successful upload
          }
        }}
      >
        {({ open }) => (
          <button className="btn btn-primary" onClick={() => open()}>
            Upload
          </button>
        )}
      </CldUploadWidget>
    </>
  );
};

export default UploadPage;
```