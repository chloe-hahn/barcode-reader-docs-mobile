---
layout: default-layout
title: Interface ImageSource - Dynamsoft Barcode Reader Android API Reference
description: This the interface ImageSource page of Dynamsoft Barcode Reader for Android SDK.
keywords: ImageSource, interface, android
needAutoGenerateSidebar: true
needGenerateH3Content: false
noTitleIndex: true
---

# ImageSource

Interface for producers of images. It can be implemented by developers to support other image sources, such as external cameras or image filesets.

How to Use:

1. Use [`BarcodeReader.setImageSource`](primary-video.md#setimagesource) to set `ImageSource` as the source of image.
2. Add code in method `getImage`. When DBR finishes the current process and trying to start decoding from another image, it will call the `getImage`.
3. Trigger [`BarcodeReader.startScanning`](primary-video.md#startscanning) to start the barcode decoding thread when all above are configured.
4. When barcode decoding thread is started, users can stop the thread by calling [`BarcodeReader.stopScanning`](primary-video.md#stopscanning)

```java
interface com.dynamsoft.dbr.ImageSource
```

| Method | Description |
| ------ | ----------- |
| `getImage` | The method for users for complete. Get image/video from external sources and out put the data as [`ImageData`](auxiliary-ImageData.md). |

## getImage

The method for users for complete which returns [`ImageData`](auxiliary-iImageData.md). When using external sources, users can generate the external image source into [`ImageData`](auxiliary-iImageData.md) and output them in method `getImage` so that the image can be recognized by the Barcode Reader.

The barcode reader will continuously use `getImage` to acquire [`ImageData`](auxiliary-iImageData.md) for barcode decoding when:

- Method [`BarcodeReader.setImageSource`](primary-video.md#setimagesource) has been configured in user's project.
- [`BarcodeReader.startScanning`](primary-video.md#startscanning) is triggered.

```java
ImageData getImage();
```

**Return Value**

An object of `ImageData`.

**Code Snippet**

Here we use CameraX as the example of the image source. The following code displays how to use CameraX to capture video frames and tranfer the video frames into [`ImageData`](auxiliary-ImageData.md).

```java
private ImageData mImageData;
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    try {
        mReader = new BarcodeReader();
    } catch (BarcodeReaderException e) {
        e.printStackTrace();
    }
    // Set image source
    mReader.setImageSource(new ImageSource() {
        @Override
        // Configure the getImage method.
        public ImageData getImageData() {
            return mImageData;
        }
    });
    // Configure the listener to receive the TextResult from the textResultCallback
    mReader.setTextResultListener(new TextResultListener() {
        @Override
        public void textResultCallback(int i, ImageData imageData, TextResult[] textResults) {
            // Add your code to execute when iTextResult is received.
        }
    }
}
// onResume start barcode decoding.
@Override
protected void onResume() {
    super.onResume();
    mReader.startScanning();
}
// onPause stop barcode decoding.
@Override
protected void onPause() {
    super.onPause();
    mReader.stopScanning();
}
// Get the buffer image from CameraX Analyzer and generate the image into iImageData.
private ImageAnalysis.Analyzer mBarcodeAnalyzer = new ImageAnalysis.Analyzer() {
    @Override
    public void analyze(@NonNull ImageProxy imageProxy) {
        try {
            if(isShowingDialog) {
                mImageData = null;
                return;
            }
            byte[] data = new byte[imageProxy.getPlanes()[0].getBuffer().remaining()];
            imageProxy.getPlanes()[0].getBuffer().get(data);
            int nRowStride = imageProxy.getPlanes()[0].getRowStride();
            int nPixelStride = imageProxy.getPlanes()[0].getPixelStride();
            ImageData imageData = new ImageData();
            imageData.bytes = data;
            imageData.width = imageProxy.getWidth();
            imageData.height = imageProxy.getHeight();
            imageData.stride = nRowStride;
            imageData.format =EnumImagePixelFormat.IPF_NV21;
            imageData.orientation = imageProxy.getImageInfo().getRotationDegrees();
            mImageData = imageData;
        } finally {
            imageProxy.close();
        }
    }
};
```