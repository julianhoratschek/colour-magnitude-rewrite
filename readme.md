# Colour Magnitude rewrite

This is a "Fan"-rewrite of the colour magnitude program of Astrophysics of CAU Kiel.
I did not do any of the fancy "maths"-stuff, but tried to put the existing functionality into a more user friendly framework.

## Requirements 📂

- Python Version 3.12 or higher
- Package-dependencies: see [requirements.txt](requirements.txt)

## Installation 📦

Clone from github

```shell
git clone https://github.com/julianhoratschek/colour-magnitude-rewrite ./your_dest_folder
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

- Paths for fits files (String, multiple files allowed in one directory):
  - path_light_short = "./data/colour/blue/"
  - path_light_long
  - path_dark_short
  - path_dark_long
  - path_flat_short
  - path_flat_long
  - path_dark_flat

- Output directory (String):
  - path_result

- Flags for corrections (Booleans):
  - do_dark: Dark correction (uses path_dark_short and path_dark_long)
  - do_flat: Flat field correction (uses path_flat_short and path_flat_long)
  - do_dark_flat: Dark correction for flat fields (uses path_dark_flat)

- Names for colour (Strings, for labels during plotting):
  - short_colour: Name for short wave colour
  - long_colour: Name for long wave colour

- Position in degrees of the observatory (Float, optional):
  - longitude = 9.112354
  - latitude  = 53.347889

- Data (float):
  - FWHM: FWHM of the major axis of stars (1D-Gaussian) in pixels; one pixel w/o binning ~0.9 arcseconds; typical seeing conditions ~2-4 arcseconds
  - ratio: ratio of FWHM_minor and FWHM_major; 0.0 means circular Gaussian
  - threshold: threshold * std = detection threshold for star finding algorithm; std is standard deviation of the sky background, i.e., read out noise + dark current noise
  - r_aperture: radius of the circular aperture to count star flux, in units of FWHM; theoretically as large as possible, but possible contamination of other stars nearby

### Navigation 📍

- MouseWheel: Zoom Image
- Ctrl + LeftMouse: Pan Image
- LeftMouse: Select/Deselect single star
- Shift + LeftMouse: Select/Deselect multiple Stars
- RightMouse: Set user defined short- and long- wave magnitudes for one star
  - Set both values to 0 to set star back to standard

- Plot via "FHD Diagram"
- Save calculated data by selecting "Save data" in Plot Window

### Colour coding 🎨

- <span style="color:green">green:</span> Selected star (default)
- <span style="color:blue">blue:</span> Selected star, labeled with user defined magnitudes
- <span style="color:red">red:</span> Deselected star
- <span style="color:orange">orange:</span> Deselected star, labeled with user defined magnitudes


