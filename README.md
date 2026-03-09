# EO Image Viewer

**A lightweight Napari-based viewer for multispectral Earth Observation imagery.**

Custom-built for EO image analysis workflows — band loading, RGB compositing, resampling, contrast control, histogram, and export. Designed around Sentinel-2 data but compatible with any multiband GeoTIFF raster.

Developed by [Flora Gabriagues](https://floragabriagues.github.io) — Optical Payload & Image Quality Engineer.

---

## What it does

A Napari viewer extended with a custom tools menu for common EO image analysis tasks:
- Load multiband rasters or directories of single-band files
- Build RGB composites from arbitrary band combinations
- Resample and restack bands at different spatial resolutions
- Control contrast manually or via histogram
- Export layers as raw data or screen render

<img width="2157" height="1549" alt="image" src="https://github.com/user-attachments/assets/1c592632-311f-4577-803b-4e7ecd349fa8" />

---

## Features & status

| Feature | Status |
|---|---|
| Multiband loading — single file | ✅ stable |
| Multiband loading — directory of band files | ✅ stable |
| Automatic band detection (Sentinel-2 naming) | ✅ stable |
| Multiscale pyramid for large images | ✅ stable |
| RGB composite from arbitrary bands | ✅ stable |
| Band resampling / restacking | ✅ stable |
| Manual contrast control | ✅ stable |
| Histogram display (per band + RGB) | ✅ stable |
| Raw export (GeoTIFF, uint16) | ✅ stable |
| Render export (PNG/JPG, contrast + gamma applied) | ✅ stable |
| FTM computation | 🚧 in progress |

---

## Usage

```bash
# Open a multiband file with specific bands (1-based index)
python viewer_napari.py /path/to/image.tif --bands 4,3,2

# Open a Sentinel-2 directory, auto-detect bands
python viewer_napari.py /path/to/S2_directory --dir

# Open a Sentinel-2 directory with specific bands
python viewer_napari.py /path/to/S2_directory --dir --bands B04,B03,B02

# Force a bin factor for preview (e.g. large images)
python viewer_napari.py /path/to/S2_directory --dir --bin 4
```

---

## Tools menu

Once the viewer is open, all tools are accessible via the **Tools** menu in the top bar:

| Tool | Description |
|---|---|
| Create Composition | Build an RGB composite from 3 selected layers |
| Resample | Resample one band to match another's resolution |
| Adjust Contrast | Set explicit min/max contrast limits |
| Display Histogram | Per-band or RGB histogram |
| Save Layer | Export as raw GeoTIFF or screen render (PNG/JPG/TIF) |
| Compute MTF | MTF computation from a selected line *(in progress)* |

---

## Resampling

The resampling tool handles mixed-resolution band stacking — for example combining Sentinel-2 10m and 20m bands into a common grid:

- **Average** — physical binning (integer factor only, e.g. 20m → 10m)
- **Nearest** — no interpolation, preserves raw values
- **Bilinear** — smooth upsampling

---

## Export modes

| Mode | Description |
|---|---|
| `raw` | Writes original pixel values (uint16 GeoTIFF) |
| `render` | Applies contrast limits + gamma, exports as seen on screen (PNG/JPG/TIF) |

---

## Tested with

- Sentinel-2 L1C and L2A products (`.jp2` bands in directory structure)
- Any multiband GeoTIFF raster readable by rasterio

---

## Dependencies

```
napari
rasterio
numpy
matplotlib
magicgui
scikit-image
imageio
dask (optional — parallel band loading)
```

Install:

```bash
pip install napari rasterio numpy matplotlib magicgui scikit-image imageio dask
```

---

## Modules

| File | Content |
|---|---|
| `viewer_napari.py` | Main viewer, tools menu, all widgets |
| `metrics.py` | Image quality metrics — FTM *(in progress)* |

---

## About

This viewer is part of my freelance activity in **optical payload performance and image quality** for Earth Observation missions.

I work with engineering teams on:
- In-orbit image quality analysis
- Calibration & validation planning
- Image processing and performance assessment tools
- Geometric and radiometric performance budgets

→ [floragabriagues.github.io](https://floragabriagues.github.io)

---

*The full toolbox, including advanced IQ metrics and customization for specific mission data formats, is available as part of consulting engagements.*
