# Calendar Rewind Restaurant Data

`restaurants.sqlite` is a derived database of dining-venue names from OpenStreetMap. Calendar Rewind, a free iOS app for looking back through events saved in Apple Calendar, bundles this same file and uses it on device as a name lookup when recognizing restaurant plans. The database is published here, on its own, under the [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/). This repository contains the database, the license text, and these notes.

It was built from the Geofabrik extract of US OpenStreetMap data, `us-261014.osm.pbf` (12,206,447,982 bytes; source timestamp 2026-10-14T20:21:12Z), downloaded from [https://download.geofabrik.de/north-america/us.html](https://download.geofabrik.de/north-america/us.html). The file records a filtered intermediate, `us-dining.osm.pbf`, produced with osmium 1.19.1, and a build time of 2026-10-15T21:24:47Z. Venue names, the OSM categories attached to them, and alternate names were kept. Names were normalized for lookup: case folded, apostrophes removed, diacritics stripped, `&` turned into `and`, and `+` and other punctuation turned into spaces. Coordinates and other map geometry were left out, so a matching name identifies a known venue name from that extract rather than a specific place. The build script is not in this repository. The source filenames and license note are stored in the database table `dataset_info`.

## Attribution and license

Restaurant data **© [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors**

The database is made available under the [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/). The file `LICENSE` is the official plain text from [https://opendatacommons.org/licenses/odbl/odbl-10.txt](https://opendatacommons.org/licenses/odbl/odbl-10.txt), linked from that page. ODbL applies to this database, not to the Calendar Rewind application source.

## What is in the database

`restaurants.sqlite` is a derived name lookup. It has no coordinates and no map geometry. A name match does not confirm a real-world visit or a specific place.


| Table             | Role                                                                                                           |
| ----------------- | -------------------------------------------------------------------------------------------------------------- |
| `names`           | Normalized venue name, display name, an occurrence count, and a name class (`standard`, `short`, or `generic`) |
| `name_categories` | OSM-style category tags for a name, with a feature count                                                       |
| `aliases`         | Alternate names pointing at a row in `names`                                                                   |
| `dataset_info`    | Build and license notes recorded when the file was created                                                     |


Categories stored in this file are:

`amenity:restaurant`, `amenity:cafe`, `amenity:fast_food`, `amenity:bar`, `amenity:pub`, `shop:bakery`, `amenity:ice_cream`, `shop:coffee`, `shop:pastry`, `amenity:food_court`, `amenity:biergarten`, `shop:ice_cream`, `amenity:juice_bar`

Alias types stored in this file are OSM-style name tags: `alt_name`, `brand`, `official_name`, `short_name`, `name:en`, `loc_name`, `name`, `alt_name:en`, `brand:en`, `int_name`.

The app’s lookup key lowercases names, strips apostrophes and diacritics, turns `&` into `and`, and turns `+` and other punctuation into spaces. `dataset_info` records that same normalization. The build script that loaded the OpenStreetMap extract is not in this repository.

## Provenance

The US OpenStreetMap extract was downloaded from Geofabrik: [https://download.geofabrik.de/north-america/us.html](https://download.geofabrik.de/north-america/us.html)

`dataset_info` records:

- source filename `us-261014.osm.pbf`
- source size `12206447982` bytes
- source timestamp `2026-10-14T20:21:12Z`
- filtered intermediate filename `us-dining.osm.pbf`
- built at `2026-10-15T21:24:47Z` with `osmium version 1.19.1`
- variant `enhanced`
- `geographic_fields` = `none`

`source_file` and `filtered_file` store those filenames only. Local build-machine paths were removed from both the app copy and this copy. The `.pbf` files were not present to re-check. The Geofabrik download is the stated origin of the extract; this repository does not add a separate Geofabrik credit.

## Download

Clone this repository, or download `restaurants.sqlite` from GitHub. The file is about 24 MB (`25632768` bytes).

SHA-256:

```text
0c9c9882cf04e9c74051ab0b515b9d6caceb953c6030e7f7f9df3a34124c6e14
```

To confirm a copy matches:

```sh
shasum -a 256 restaurants.sqlite
```

