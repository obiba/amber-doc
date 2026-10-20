.. _cb_large_select:

How to make a select with a lot of options?
===========================================

When there are a lot of possible options it can be tricky to design a user friendly selection field.

Step 1 - Select Auto complete field
-----------------------------------

There several type of fields for selecting among a list of options:

* Single/Multiple choice
* Dropdown
* Auto complete

The **Auto complete** is the most appropriate because there is not the problem of rendering a long list of proposed options. The field works as a filter: user enters at least two letters to trigger the display of the ten first items matching the entered text.

Step 2 - Prepare the options
----------------------------

The options will be defined in file. The file format is CSV (comma separated values, with file suffix ``.csv`` or ``.txt``) or TSV (tab separated values, with file suffix ``.tsv``). No header is expected. The first value if the option value (the data collected), the second one is the option label (can be a translation key for a multilanguage form).

Example of options file (CSV):

.. code::

  J0Y,Abitibi-Témiscamingue-Est (Radisson)
  J0Z,Abitibi-Témiscamingue-Ouest (Guigues)
  H2C,Ahuntsic Central
  H2M,Ahuntsic East
  H2B,Ahuntsic North
  H2N,Ahuntsic Southeast
  H3L,Ahuntsic Southwest
  H0M,Akwesasne Region (Akwesasne)
  G8M,Albanel
  G8E,Alma North
  G8B,Alma Southeast
  G8C,Alma Southwest
  J9T,Amos
  G5J,Amqui
  H1K,Anjou East
  H1J,Anjou West
  G0R,Appalaches (La Pocatière)

When the value and the label are the same, it is possible to provide a simple list:

.. code::

  Hôpital chinois de Montréal
  Hôpital géneral juif
  Hôpital Santa Cabrini
  Hôpital Mont-Sinaï - Montréal
  Hôpital de Lachine
  Hôpital Richardson
  Hôpital Marie-Clarac
  Institut de réadaptation Gingras-Lindsay de Montréal
  Hôpital neurologique de Montréal
  Centre gériatrique Maimonides Donald Berman
  Hôpital Sainte-Anne

Step 3 - Upload options
-----------------------

The **Options** setting proposes to **Upload options**: select the options file and the options values and labels will be automatically added.
