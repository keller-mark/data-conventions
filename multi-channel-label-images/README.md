# multi-channel-label-images

## Use case

Multiple types of segmentation bitmasks for a single histology image (e.g., glomeruli, tubules, arteries, cells).

## Convention

Label images stored in OME-TIFF or OME-Zarr:

- Each channel `c` represents a different type of observation
- Channel names indicate the type of observation contained in the channel
- Pixel value `0` is used to indicate background
- Segmentation for observation with index $i \in [1, ..., N_c]$ where $N_c$ is the number of observations in channel `c`

### Alignment with per-observation feature values

