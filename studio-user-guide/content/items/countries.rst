.. _item_countries:

Countries
=========

``format: "countries"`` is a searchable select of country codes, single or multiple.

By default, the countries are listed with their ISO 3166-1 alpha-3 code (such as ``CAN`` for Canada) and their English or French name. The ``countries`` setting of the control replaces this list: a ``[{ code, name }]`` array, or a ``{ locale: [...] }`` map of such arrays keyed by language (the language of the form is used).

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

============= ============================================= =======================
Entry         Schema                                        UI schema
============= ============================================= =======================
**Countries** ``{"type": "string", "format": "countries"}`` ``{"type": "Control"}``
============= ============================================= =======================

Schema
------

The schema shapes that select this renderer:

======================================================================================================== ========================================
Schema                                                                                                   Description
======================================================================================================== ========================================
``{ "type": "string" } + format: "countries" \| "obibaCountriesUiSelect"``                               One country, searchable by name or code.
``{ "type": "array", "items": { "type": "string" } } + format: "countries" \| "obibaCountriesUiSelect"`` Several countries, displayed as chips.
======================================================================================================== ========================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============= =============== ======= ===============================================================================================================================================================================================================================================================================================================================
Setting       Type            Default Description
============= =============== ======= ===============================================================================================================================================================================================================================================================================================================================
``countries`` Array \| Object         The ``[{ code, name }]`` list, or a ``{ locale: [...] }`` map (the current vue-i18n locale is used). Defaults to ``config.countries`` of ``QJsonForm``, then a ``jsonforms-countries`` provide of the application. The ``countryCodes`` export of the library holds the ISO 3166-1 alpha-3 codes with english and french names.
Other         any                     Every other option is passed as a prop to `QSelect <https://quasar.dev/vue-components/select#qselect-api>`__.
============= =============== ======= ===============================================================================================================================================================================================================================================================================================================================

Data
----

A country code, or an array of codes (an emptied selection stores ``undefined``).

.. code:: json

   { "country": "CAN", "countries": ["CAN", "FRA"] }

See also the `Countries <https://www.obiba.org/quasar-json-form/#/controls/countries>`__ page of the Quasar JSON Form documentation, with live examples.
