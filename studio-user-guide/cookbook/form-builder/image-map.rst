.. _cb_fe_image_map:

How to make an image map?
=========================

A selection field can be coupled with an image: the options are areas of the image that are clicked to be selected, for instance the parts of a body map.

Step 1 - Add an Image map control
---------------------------------

From the *Controls* menu of the form builder, add an **Image map** control (see :ref:`item_image_map`). For a multiple selection, add a **Multiple select** and set its ``format`` setting to ``image-map``.

Step 2 - Set the image
----------------------

In the *Settings* section, set the **image**. The supported image formats are JPEG, PNG and WebP. The image can be integrated to the form in different ways:

* **Using a web link**, which must be publicly accessible (i.e. no authentication/authorization required). This makes the form unfunctional when offline: network access is required to download the image when the form is administered.
* **Embedded in the form**, by choosing a local image file. The image data are directly encoded in the form, which makes the image available while offline. As this makes the form larger, prefer images of a reasonable size.

Step 3 - Define the choices and their areas
-------------------------------------------

In the *Choices* section, each choice has a value, a label, and an area of the image:

* the **shape**: ``rect`` (rectangle), ``circle`` or ``poly`` (polygon),
* the **coordinates**, in the pixels of the image: ``x1, y1, x2, y2`` for a rectangle (top-left and bottom-right corners), ``cx, cy, r`` for a circle (center and radius), ``x1, y1, x2, y2, x3, y3, ...`` for a polygon.

There are some free online tools that can help with drawing these areas, see for instance `image-map.net <https://www.image-map.net/>`_.

By default, a select of the same choices is displayed under the image, in sync with the areas: the ``select`` setting hides it. The ``outline`` setting outlines all the areas, to show where they are, and the ``color`` setting is the color of the hovered and selected areas.

.. tip::
  To select among pictures rather than areas of a single picture, use the **Images** control (see :ref:`item_images`): each choice has its own image.
