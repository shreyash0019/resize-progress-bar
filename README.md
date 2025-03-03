# Image Resizing with Progress Bar

This script allows you to resize multiple images at once and shows a progress bar indicating the progress of the resizing process.

## Installation

To install the necessary libraries, run the following commands:

```sh
pip install tqdm
pip install Pillow
```

## Usage

1. Place the script (`image_resize.py`) in the directory where your images are located.
2. Run the script using Python:

```sh
python image_resizing.py
```

3. Enter the path to the images when prompted.
4. Enter the desired size (height, width) when prompted.

The resized images will be saved in a folder named `resize` within the specified directory.

## Example

```sh
Enter Path to images : /path/to/your/images
Size Height , Width : 800,600
```

The above example will resize all images in the specified directory to a size of 800x600 pixels and save them in the `resize` folder.

## Code

```python
from tqdm import tqdm
from PIL import Image
import os
from time import sleep

def Resize_image(size, image):
    if os.path.isfile(image):
        try:
            im = Image.open(image)
            im.thumbnail(size, Image.ANTIALIAS)
            im.save("resize/" + str(image) + ".jpg")
        except Exception as ex:
            print(f"Error: {str(ex)} to {image}")

path = input("Enter Path to images : ")
size = input("Size Height , Width : ")
size = tuple(map(int, size.split(",")))
os.chdir(path)
list_images = os.listdir(path)
if "resize" not in list_images:
    os.mkdir("resize")
for image in tqdm(list_images, desc="Resizing Images"):
    Resize_image(size, image)
    sleep(0.1)
print("Resizing Completed!")
```
