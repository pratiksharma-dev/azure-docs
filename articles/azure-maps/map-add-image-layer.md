---
title: Add an Image layer to a map | Microsoft Azure Maps
description: Learn how to add images to a map. See how to use the Azure Maps Web SDK to customize image layers and overlay images on fixed sets of coordinates.
author: eriklindeman
ms.author: eriklind
ms.date: 07/29/2019
ms.topic: conceptual
ms.service: azure-maps
ms.custom: codepen, devx-track-js
---

# Add an image layer to a map

This article shows you how to overlay an image to a fixed set of coordinates. Here are a few examples of different images types that can be overlaid on maps:

* Images captured from drones
* Building floorplans
* Historical or other specialized map images
* Blueprints of job sites
* Weather radar images

> [!TIP]
> An [ImageLayer](/javascript/api/azure-maps-control/atlas.layer.imagelayer) is an easy way to overlay an image on a map. Note that browsers might have difficulty loading a large image. In this case, consider breaking your image up into tiles, and loading them into the map as a [TileLayer](/javascript/api/azure-maps-control/atlas.layer.tilelayer).

The image layer supports the following image formats:

- JPEG
- PNG
- BMP
- GIF (no animations)

## Add an image layer

The following code overlays an image of a map of Newark, New Jersey, from 1922 on the map. An [ImageLayer](/javascript/api/azure-maps-control/atlas.layer.imagelayer) is created by passing a URL to an image, and coordinates for the four corners in the format `[Top Left Corner, Top Right Corner, Bottom Right Corner, Bottom Left Corner]`.

```javascript
//Create an image layer and add it to the map.
map.layers.add(new atlas.layer.ImageLayer({
    url: 'newark_nj_1922.jpg',
    coordinates: [
        [-74.22655, 40.773941], //Top Left Corner
        [-74.12544, 40.773941], //Top Right Corner
        [-74.12544, 40.712216], //Bottom Right Corner
        [-74.22655, 40.712216]  //Bottom Left Corner
    ]
}));
```

Here's the complete running code sample of the preceding code.

<br/>

<iframe height='500' scrolling='no' title='Simple Image Layer' src='//codepen.io/azuremaps/embed/eQodRo/?height=500&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' loading="lazy" allowtransparency='true' allowfullscreen='true'>See the Pen <a href='https://codepen.io/azuremaps/pen/eQodRo/'>Simple Image Layer</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Import a KML file as ground overlay

This sample demonstrates how to add KML ground overlay information as an image layer on the map. KML ground overlays provide north, south, east, and west coordinates, and a counter-clockwise rotation. But, the image layer expects coordinates for each corner of the image. The KML ground overlay in this sample is for the Chartres cathedral, and it's sourced from [Wikimedia](https://commons.wikimedia.org/wiki/File:Chartres.svg/overlay.kml).

The code uses the static `getCoordinatesFromEdges` function from the [ImageLayer](/javascript/api/azure-maps-control/atlas.layer.imagelayer) class. It calculates the four corners of the image using the north, south, east, west, and rotation information of the KML ground overlay.

<br/>

<iframe height='500' scrolling='no' title='KML Ground Overlay as Image Layer' src='//codepen.io/azuremaps/embed/EOJgpj/?height=500&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' loading="lazy" allowtransparency='true' allowfullscreen='true'>See the Pen <a href='https://codepen.io/azuremaps/pen/EOJgpj/'>KML Ground Overlay as Image Layer</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

> [!TIP]
> Use the `getPixels` and `getPositions` functions of the image layer class to convert between geographic coordinates of the positioned image layer and the local image pixel coordinates.

## Customize an image layer

The image layer has many styling options. Here's a tool to try them out.

<br/>

<iframe height='700' scrolling='no' title='Image Layer Options' src='//codepen.io/azuremaps/embed/RqOGzx/?height=700&theme-id=0&default-tab=result' frameborder='no' loading="lazy" allowtransparency='true' allowfullscreen='true'>See the Pen <a href='https://codepen.io/azuremaps/pen/RqOGzx/'>Image Layer Options</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Next steps

Learn more about the classes and methods used in this article:

> [!div class="nextstepaction"]
> [ImageLayer](/javascript/api/azure-maps-control/atlas.layer.imagelayer)

> [!div class="nextstepaction"]
> [ImageLayerOptions](/javascript/api/azure-maps-control/atlas.imagelayeroptions)

See the following articles for more code samples to add to your maps:

> [!div class="nextstepaction"]
> [Add a tile layer](./map-add-tile-layer.md)
