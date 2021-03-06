# jlcpcb-eagle
EAGLE cad helpers for JLCPCB (https://jlcpcb.com) production and assembly services

## General info

Rules and scripts have been tested under EAGLE cad 9.5.

They're provided AS IS, with no warranty. Any feedback is greatly appreciated and
can be provided via issue tickets.

This repo is not endorsed by JLCPCB.

### Installation

Copy each file in their respective folders (USER_HOME/Documents/EAGLE/).

## CAM jobs

* cam/jlcpcb-2layers.cam: 2-layers version

The jobs follow the naming guidelines defined here: https://support.jlcpcb.com/article/29-suggested-naming-patterns
They also include tCream/bCream solderpaste layers that could be used for the stencil service.

## Design rules

* design rules/jlcpcb-2layers.dru: 2-layers version, 35u copper, 1.6mm board thickness

Mainly based on EAGLE's standard design rules, it adds the declared JLCPCB's capabilities listed
here: https://jlcpcb.com/capabilities/Capabilities

Note: annular ring for pads aren't minimal, in order to allow proper solderability of TH components

## ULPs

* ulps/jlcpcb_smta_exporter.ulp: BOM (bill of materials) / CPL (pick&place) exporter

The smta exporter ULP can be used to quicken the process of creating the required files for the
SMT assembly service.

Observe the following:

1. it must be executed from the board editor
2. it asks for the layer to process (either top or bottom), this must be consistent with the ordering process
3. it asks for a directory where to export the two files
4. the two files will be named ```<boardname>_<side>_bom.csv``` and ```<boardname>_<side>_cpl.csv```
5. components rotations are sketchy and must be visually checked on the online gerber viewer once uploaded the files

The ULP can extract LCSC part ordering numbers from the packages attributes. The attribute must be named _LCSC_PART_ or _LCSC_ and it should contain the order code found in the parts library https://jlcpcb.com/client/index.html#/parts (eg: C25804).

The ULP can also manually rotate the angle in the CPL output file. The attribute must be named _JLC_ROTATION_. For example, if a part's angle in set to 90 and it's attribute _JLC_ROTATION_ is set to 180, the angle in the final CPL file will be set to 270.
