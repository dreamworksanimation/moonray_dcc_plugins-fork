# moonray_dcc_plugins - part of the [MoonRay](https://github.com/OpenMoonRay/openmoonray) project

Policies concerning [Governance](https://github.com/OpenMoonRay/openmoonray/blob/main/GOVERNANCE.md), [Code of Conduct](https://github.com/OpenMoonRay/openmoonray/blob/main/CODE_OF_CONDUCT.md), and [Contribution](https://github.com/OpenMoonRay/openmoonray/blob/main/CONTRIBUTING.md) are available in the overarching MoonRay project, defined in the [OpenMoonRay/openmoonray GitHub repository superproject](https://github.com/OpenMoonRay/openmoonray).

This repository contains plugins for DCC apps to support MoonRay.

# Houdini 
## Installation

Include the folders inside of the houdini folder into your HOUDINI_PATH by copying them into a folder already sourced or adding them to the HOUDINI_PATH environment variable

see https://www.sidefx.com/docs/houdini/basics/config.html

- Add to Variable:
  add the openmoonray/plugin/houdini/ folder to your HOUDINI_PATH
  ```
      HOUDINI_PATH = $HOUDINI_PATH:<openmoonray_install_dir>/plugin/houdini
  ```

- or copy the folders inside into your local houdini:
  ```
      cp -r <openmoonray_install_dir>/plugin/houdini/* ~/houdini19.5/
  ```

Note : if you folow the cmake build and install instructions in the root repo, this happens as an installation step. 
the supplied `<openmoonray_install_dir>/scripts/{macOS, Rocky9}/setupHoudini.sh` will set up the correct paths.


## Updating

We provide a script `moonray_dcc_plugins/scripts/update_hdas.py` to update the existing hdas and ds files from new moonray modifications.

Runtime dependencies:
    - hython / hou   (Houdini writes the .hda and .ds files itself)
    - `rdl2_json_exporter` on $PATH, with $RDL2_DSO_PATH set to the proxy DSOs
    - pxr Python modules (optional; falls back to static output tags)

1. Set up environment:
Use houdini shell, or source their setup.sh, for example:
```
source <houdini_install_dir>/Houdini20.0.751/Frameworks/Houdini.framework/Versions/Current/Resources/houdini_setup
```

Add the moonray environment:
```
source <openmoonray_install_dir>/scripts/{macOS, Rocky9}/setupHoudini.sh
```

2. run script

```
cd <moonray_dcc_plugins_repo_root>
hython scripts/update_hdas.py --output-dir ./houdini
```

3. install
```
cp houdini/moonray_nodes.json <openmoonray_install_dir>/plugin/houdini
cp -r houdini/{otls,soho,python*} <openmoonray_install_dir>/plugin/houdini
```


