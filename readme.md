# Colour Magnitude rewrite

This is a "Fan"-rewrite of the colour magnitude program of Astrophysics of CAU Kiel.
I did not do any of the fancy "maths"-stuff, but tried to put the existing functionality into a more user friendly framework.

## Requirements 📂

- Python Version 3.12 or higher
- Package-dependencies: see [requirements.txt](requirements.txt)

## Installation 📦

Clone from github

```shell
git clone https://github.com/julianhoratschek/colour-magnitude-rewrite.git ./your_dest_folder
```

Enter directory

```shell
cd ./your_dest_folder/
```

Create python virtual environment

```shell
python -m venv .venv
```

Enter python virtual environment (please consult the [online docs on how to enter it with your respective shell](https://docs.python.org/3/library/venv.html#how-venvs-work))

```shell
# Using fish:
source .venv/bin/activate.fish

# For Powershell this would be:
# .venv/Scripts/Activate.ps1
```

Install dependencies

```shell
pip install -r requirements.txt
```

Done 🎉

## Usage 🔨

- setup by defining values in [input_cmd.toml](input_cmd.toml) in the same directory as main.py
- Have data ready at paths defined in input_cmd.toml
- Run

```shell
python main.py
```

### input_cmd.toml 💡

Please follow standard [toml-language specs](https://toml.io/en/).

#### Paths for fits files

Each directory can contain multiple FITS-Files, all of those files will be loaded

| Variable         | Value | Example               |
| ---------------- | ----- | --------------------- |
| path_light_short | Path  | "./data/colour/blue/" |
| path_light_long  | Path  |                       |
| path_dark_short  | Path  |                       |
| path_dark_long   | Path  |                       |
| path_flat_short  | Path  |                       |
| path_flat_long   | Path  |                       |
| path_dark_flat   | Path  |                       |

#### Output directory

| Variable    | Value | Example      |
| ----------- | ----- | ------------ |
| path_result | Path  | "./results/" |

#### Flags for corrections

| Variable     | Value                | Description                                                    |
| ------------ | -------------------- | -------------------------------------------------------------- |
| do_dark      | Boolean (true/false) | Dark correction (uses path_dark_short and path_dark_long)      |
| do_flat      | Boolean              | Flat field correction (uses path_flat_short and path_flat_long |
| do_dark_flat | Boolean              | Dark correction for flat fields (uses path_dark_flat)          |

#### Names for colour

These values will be displayed during plotting

| Variable     | Value  | Description                |
| ------------ | ------ | -------------------------- |
| short_colour | String | Name for short wave colour |
| long_colour  | String | Name for long wave colour  |

#### Position in degrees of the observatory

| Variable  | Value | Example   |
| --------- | ----- | --------- |
| longitude | Float | 9.112354  |
| latitude  | Float | 53.347889 |

#### Data

| Variable   | Value | Description                                                                                                                                                  |
| ---------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| FWHM       | Float | FWHM of the major axis of stars (1D-Gaussian) in pixels; one pixel w/o binning ~0.9 arcseconds; typical seeing conditions ~2-4 arcseconds                    |
| ratio      | Float | ratio of FWHM_minor and FWHM_major; 0.0 means circular Gaussian                                                                                              |
| threshold  | Float | threshold * std = detection threshold for star finding algorithm; std is standard deviation of the sky background, i.e., read out noise + dark current noise |
| r_aperture | Float | radius of the circular aperture to count star flux, in units of FWHM; theoretically as large as possible, but possible contamination of other stars nearby   |

### Navigation 📍

 | Input                    | Action                                                          |
 | ------------------------ | --------------------------------------------------------------- |
 | MouseWheel               | Zoom Image                                                      |
 | Ctrl + LeftMouse         | Pan Image                                                       |
 | LeftMouse                | Select/Deselect single star                                     |
 | Shift + LeftMouse (Drag) | Select/Deselect multiple Stars                                  |
 | RightMouse               | Set user defined short- and long- wave magnitudes for one star. | Set both values to 0 to set star back to standard |

- Plot via "FHD Diagram"
- Save calculated data by selecting "Save data" in Plot Window

### Colour coding 🎨

- <span style="color:green">green:</span> Selected star (default)
- <span style="color:blue">blue:</span> Selected star, labeled with user defined magnitudes
- <span style="color:red">red:</span> Deselected star
- <span style="color:orange">orange:</span> Deselected star, labeled with user defined magnitudes


