---
title: Input files
layout: default
nav_order: 5
---
Input files
==================

Load script
-----------

The load script is defined on the settings page (URL field). Can for example be a <b>php</b> script.

The following parameters are supplied:

- key - The secret field defined on the settings page, can be used if to restrict access to the information to be loaded
- what - Will be either "sitelist" or "doc". Defines the expected answer as describe below.
- ver - only used for testing so can be ignored


Sites (answer when <b>what</b> = sitelist)
----------------------------

A json formatted file containing two sections <b>config</b> and <b>sites</b>.

<b>sitecolors</b> define the colors of the site icons ![BasestationIcon]. "l1" is the transmitt waves and "l2" is the tower.
Here RGBA colour codes are used.

<b>areacolors</b> define the colors for the tracking area borders. Likewise using RGBA colour codes.

<b>sites</b> is an array of elements, one per site. Using the defined <b>sitecolors</b> and <b>areacolors</b>.

- easting/northing or lat/long can be used
- G3, G4 and G5 represents technologies 3G, 4G and 5G
- category can be "Customer" or "Public" (can be filtered on the settings page)
- pd - Planned (operational) Date
- opd - Operational Date
- ptd - Planned Termination Date
- dt - Termination Date
- area - refers back to the defined areas
- icon - refers to the defined icons
- status - "Active" or "inActive" (can be filtered on the settings page)
- feed - If set to another site ID a line will be drawn between the sites.

```json
{
  "config": {
    "sitecolors": {
      "GrayOrange": {
        "l1": "#FF7A3380",
        "l2": "#7F8C8D80"
      },
      "GrayBlack": {
        "l1": "#00000080",
        "l2": "#7F8C8D80"
      },
      "GreenOrange": {
        "l1": "#FF7A33ff",
        "l2": "#46AE00ff"
      },
      "GreenIndigo": {
        "l1": "#E033FFff",
        "l2": "#46AE00ff"
      }
    },
    "areacolors": {
      "10": "#2C3335FF",
      "11": "#2C3335FF",
      "12": "#ff33ecFF",
      "13": "#ff33ecFF"
    }
  },
  "sites": [
    {
      "id": "1001",
      "name": "Site name",
      "easting": 1767300,
      "northing": 7241400,
      "lat": null,
      "long": null,
      "bo": "Building owner",
      "mo": "Mast owner",
      "trm": "Transmission supplier",
      "feed": "null or another site id",
      "sitetype": "site category",
      "G3": {
        "icon": "GrayOrange",
        "area": "10",
        "hw": "RBS6201",
        "opd": "2003-10-17",
        "td": "2022-03-02",
        "status": "Closed",
        "ptd": "2022-03-02",
        "category": "Public"
      },
      "G4": {
        "icon": "GreenBlack",
        "area": "11",
        "pd": "2025-01-01",
        "category": "Public",
        "status": "Active"
      },
      "G5": {
        "icon": "GreenOrange",
        "area": "12",
        "pd": "2025-01-01",
        "category": "Public",
        "status": "Active"
      }
    }
  ]
}
```


Documentation (answer when <b>what</b> = doc)
------------------------------------

An sqlite database created as follows.

- <b>CREATE TABLE</b> docs (siteid TEXT, type TEXT, file BLOB);

Currently the <b>type</b> field is unused and only UTF16 encoded text are supported in the <b>file</b> field.

Typlicy using something like <b>iconv -f iso8859-1 -t utf-16</b>


[BasestationIcon]: {{ "assets/images/celltower.png" | relative_url }}
