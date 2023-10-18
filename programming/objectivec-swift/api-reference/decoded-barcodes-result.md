---
layout: default-layout
title: DSDecodedBarcodesResult Class - Dynamsoft Barcode Reader iOS Edition
description: The DSDecodedBarcodesResult class represents the result of a barcode reading process. It provides access to information about the decoded barcodes, the source image, and any errors that occurred during the barcode reading process.
keywords: GetOriginalImageHashId, GetItemsCount, GetErrorCode, DSDecodedBarcodesResult, api reference
needAutoGenerateSidebar: true
needGenerateH3Content: true
breadcrumbText: DSDecodedBarcodesResult
permalink: /programming/objectivec-swift/api-reference/decoded-barcodes-result.html
---

# DSDecodedBarcodesResult Class

The `DSDecodedBarcodesResult` class represents the result of a barcode reading process. It provides access to information about the decoded barcodes, the source image, and any errors that occurred during the barcode reading process.

## Definition

*Assembly:* DynamsoftBarcodeReader.framework

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@interface DSDecodedBarcodesResult : NSObject
```
2. 
```swift
class DecodedBarcodesResult : NSObject
```

## Attributes

| Attributes    | Type | Description |
| ------------- | ---- | ----------- |
| [`originalImageHashId`](#originalimagehashid) | *NSString \** | The hash id of the source image. You can use this ID to get the source image via IntermediateResultManager class. |
| [`originalImageTag`](#originalimagetag) | *DSImageTag \** | The tag of the source image. |
| [`items`](#items) | *NSArray<DSBarcodeResultItem\*> \** | An array of DSBarcodeResultItems, which are the basic unit of the captured results. |
| [`rotationTransformMatrix`](#rotationtransformmatrix) | *CGAffineTransform* |Get the rotation transformation matrix of the original image relative to the rotated image. |
| [`errorCode`](#errorcode) | *NSInteger* | Get the error code of this result. |
| [`errorMessage`](#errormessage) | *NSString \** | Get the error message of this result. |

## originalImageHashId

The hash id of the source image. You can use this ID to get the source image via IntermediateResultManager class.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property(nonatomic, copy, readonly) NSString *originalImageHashId;
```
2. 
```swift
var originalImageHashId: String? { get }
```

## originalImageTag

The tag of the source image.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property(nonatomic, readonly) DSImageTag *originalImageTag;
```
2. 
```swift
var originalImageTag: DSImageTag? { get }
```

## items

An array of DSBarcodeResultItems, which are the basic unit of the captured results.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property(nonatomic, nullable, readonly) NSArray<DSBarcodeResultItem *> *items;
```
2. 
```swift
var items: [DSBarcodeResultItem]? { get }
```

## rotationTransformMatrix

Get the rotation transformation matrix of the original image relative to the rotated image.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property(nonatomic, assign, readonly) CGAffineTransform rotationTransformMatrix;
```
2. 
```swift
var rotationTransformMatrix: CGAffineTransform { get }
```

### errorCode

Get the error code of this result. A `DecodedBarcodesResult` will carry error information when the license module is missing or the process timeout.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property (nonatomic, assign, readonly) NSInteger errorCode;
```
2. 
```swift
var errorCode: Int { get }
```

### errorMessage

Get the error message of this result. A `DecodedBarcodesResult` will carry error information when the license module is missing or the process timeout.

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
@property (nonatomic, assign, readonly) NSString * errorMessage;
```
2. 
```swift
var errorMessage: String? { get }
```