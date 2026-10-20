.. _cb_image_map:

How to make an image map?
=========================

A selection field can be coupled with an image. When selected, areas of this image will be highlighted.


Step 1 - Add an Image Select Item
---------------------------------

Add an item and select the **Image select** type.

The supported image formats are the ones that are supported by web browsers, mainly PNG, JPEG and GIF. The image can be integrated to the form in different ways:

* **Using a web link**, which must be publicly accessible (i.e. no authentication/authorization required). This makes the form unfunctional when offline: network access is required to download the image when the form is administered.

* **Embeded in the form**. The binary data of the image are directly encoded in the form, which makes the image available while in offline mode. The encoding process is done by Amber Studio by selecting a local image file to upload.

Step 2 - Add Image Areas
------------------------

Once an image is defined, it is required to define areas on this image that will be used for option selection. An image area is defined by:

* **A value**, which is the stored value when the area is selected. It must match the value of one of the options.
* **A color**, in `any of the supported CSS color formats <https://developer.mozilla.org/en-US/docs/Web/CSS/color_value>`_.
* **A serie of points** that forms a polygon (circle and rectangle shapes are not supported). Each point is defined by a coordinate ``x,y``. The serie of point coordinates are to be separated by commas "," or space characters: for instance ``x1,y1,x2,y2,x3,y3`` or ``x1,y1 x2,y2 x3,y3``. There are some free online tools that can help with drawing these polygons, see for instance `image-map.net <https://www.image-map.net/>`_.

The image areas can be entered manually or uploaded from a file. The file format is CSV (comma separated values, with file suffix ``.csv`` or ``.txt``) or TSV (tab separated values, with file suffix ``.tsv``). No header is expected.

Example of image areas file (CSV format), with space-separated coordinates:

.. code::

  1,#ccc,0,0 150,0 150,750 0,750
  2,#f8bbd0,150,0 300,0 300,750 150,750
  3,#c8e6c9,345,0 495,0 495,750 345,750
  4,#ffe0b2,495,0 645,0 645,750 495,750

Example of image areas file (TSV format), with comma-separated coordinates:

.. code::

  1 #ccc    0,0,150,0,150,750,0,750
  2 #f8bbd0 150,0,300,0,300,750,150,750
  3 #c8e6c9 345,0,495,0,495,750,345,750
  4 #ffe0b2 495,0,645,0,645,750,495,750
