## Pseudocolor any Grayscale Image

This function pseudocolors any grayscale image to custom colormap. An optional mask can leave background out in the
pseudocolored image. Additionally, optional maximum and minimum values can be specified. When `pcv.params.debug='print'` 
then the image gets saved to `pcv.params.debug_outdir`. 

**plantcv.pseudocolor**(*gray_img, obj=None, mask=None, background="image", cmap=None, min_value=0, max_value=255, dpi=None, axes=True, colorbar=True*)

**returns** pseudocolored image that can be saved with `pcv.print_image`

- **Parameters:**
    - gray_img   - Grayscale image data
    - obj        - Single or grouped contour object (optional), if provided the pseudocolored image gets cropped down to the region of interest.
    - mask       - Binary mask made from selected contours
    - background - Background color/type. Options are "image" (gray_img), "white", or "black". A mask must be supplied.
    - cmap       - Custom colormap, see [here](https://matplotlib.org/tutorials/colors/colormaps.html) for tips on how to choose a colormap in Matplotlib.
    - min_value  - Minimum value (optional) for range of the colorbar.
    - max_value  - Maximum value (optional) for range of the colorbar.
    - dpi        - Dots per inch for image if printed out (optional, if dpi=None then the default is set to 100 dpi).
    - axes       - If False then the title, x-axis, and y-axis won't be displayed (default axes=True).
    - colorbar   - If False then the colorbar won't be displayed (default colorbar=True)
- **Context:**
    - Used to pseudocolor any grayscale image to custom colormap
- **Example use:**
    - [Interactive Documentation](https://mybinder.org/v2/gh/danforthcenter/plantcv-binder.git/master?filepath=notebooks%2FpsII_tutorial.ipynb)

**Original grayscale image**

![Screenshot](img/documentation_images/pseudocolor/original_grayscale.jpg)

**Mask**

![Screenshot](img/documentation_images/pseudocolor/mask.jpg)


```python

from plantcv import plantcv as pcv

pcv.params.debug='plot'

# Pseudocolor an image with 'viridis' colormad
pseudo_img = pcv.pseudocolor(gray_img=img, obj=None, mask=None, cmap='viridis', min_value=0, max_value=255)

# Pseudocolor the same image but include the mask and limit the range of values
pseudo_img_masked = pcv.pseudocolor(gray_img=img, obj=None, mask=mask, background="white", cmap='viridis', min_value=30, max_value=200)

# Save the masked and pseudocolored image
pcv.print_image(pseudo_img_masked, 'nir_tv_z300_L1_pseudocolored.png')

# Pseudocolor the masked area and plot on the grayscale background
pseudo_img_on_input = pcv.pseudocolor(gray_img=img, obj=None, mask=mask, background="image", cmap="viridis")

# Print out a pseudocolored image with cropping enabled, axes disabled, and higher dpi value.
pcv.params.debug='print'
pseudo_crop_no_axes = pcv.pseudocolor(gray_img=img, obj=obj, mask=mask, background=="white", cmap='viridis', dpi=200, axes=False)

# Use a black background instead
pseudo_img_black_bkgd = pcv.pseudocolor(gray_img=img, obj=None, mask=mask, background="black", cmap='viridis')

simple_pseudo_img = pcv.pseudocolor(gray_img=img, obj=None, mask=mask, background="image", axes=False, colorbar=False, cmap='viridis')

```


**Pseudocolored Image**

![Screenshot](img/documentation_images/pseudocolor/pseudo_nomask.jpg)

**Pseudocolored, background="white"**

![Screenshot](img/documentation_images/pseudocolor/pseudo_img.jpg)

**Pseudocolored, background="image"**

![Screenshot](img/documentation_images/pseudocolor/pseudo_onimage.jpg)

**Pseudocolored, Cropped, Disabled Axes Image**

![Screenshot](img/documentation_images/pseudocolor/pseudo_cropped.jpg)

**Pseudocolored, background="black"**

![Screenshot](img/documentation_images/pseudocolor/pseudo_black_bkgd.jpg)

**Pseudocolored, Plotted on Input Image (no axes or colorbar)**

![Screenshot](img/documentation_images/pseudocolor/pseudo_onimage_simple.jpg)