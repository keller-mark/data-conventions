# multi-channel-label-images

## Use case

Multiple types of segmentation bitmasks for a single histology image (e.g., glomeruli, tubules, arteries, cells).

## Convention

Label images stored in OME-TIFF or OME-Zarr:

- Each channel `c` represents a different type of observation
- Channel names indicate the type of observation contained in the channel
- Pixel value `0` is used to indicate background
- Segmentation for observation with index $i \in [1, ..., O_c]$ where $O_c$ is the number of observations in channel `c`

### Alignment with per-observation feature values

Each observation may be associated with feature values (i.e., an observation-by-feature matrix for each channel with shape $O_c \times F_c$ )

These observation-by-feature matrices should be stored in a MuData object `mdata`:
- Modality keys must correspond to the channel names in the label image
- Within the AnnData object for each image channel `c`, the `obs` index values must match (i.e., have the same ordering as) the pixel value identifiers in the label image
  - i.e., `mdata.mod[get_channel_name(c)].obs.index = list(range(1, mdata.mod[get_channel_name(c)].shape[0]+1))` 

#### CSV alternative

Alternatively, one CSV per image channel can be provided. The index of each CSV must also match the observation index values in the pixels of the label image. Note that when using the multi-CSV representation, there must be a manual mapping from CSV files to label image channels.
