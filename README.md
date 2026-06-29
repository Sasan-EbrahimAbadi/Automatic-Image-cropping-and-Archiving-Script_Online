# Automatic-Image-cropping-and-Archiving-Script_Online

A Bash script that continuously monitors a directory of screenshots. Once a specified number of images has been collected, it automatically crops each image, compresses them into a ZIP archive, removes the original images, and creates a new empty directory for the next batch.

## Overview

This script automates the post-processing of captured images by:

Continuously monitoring an image directory.

Waiting until at least 108 images are available.

Cropping each image to a 256 × 256 pixel region.

Compressing all processed images into a ZIP archive.

Removing the original images after successful compression.

Creating a fresh directory for the next collection cycle.

Repeating the process indefinitely.

This workflow is useful for long-running data collection projects where images are continuously generated and need to be organized into manageable batches.
___________________________________________

## Step 1: Initialize Archive Counter

x=0

The variable x is used to number each generated ZIP archive.

Example:

photo0.zip

photo1.zip

photo2.zip
__________________________________________
## Step 2: Monitor the Directory

while true

The script runs indefinitely, repeatedly checking the number of images in the directory.
__________________________________________
## Step 3: Count Images

ls -1 /home/Local_address/photo | wc -l

Counts how many files are currently stored in:

/home/Local_address/photo

When the count reaches 108 or more, processing begins.
___________________________________________
## Step 4: Crop Every Image

convert input.bmp -crop 256x256+0+0 output.bmp

Each image is cropped using ImageMagick.

Crop parameters:

Width: 256 pixels

Height: 256 pixels

X Offset: 0

Y Offset: 0

This extracts the upper-left 256 × 256 region of each image.
_______________________________________
## Step 5: Create ZIP Archive

zip -rm photo0.zip photo

Options used:

-r : recursively archive the directory.

-m : move files into the archive (delete originals after successful compression).

Example output:

zipphoto/

├── photo0.zip

├── photo1.zip

├── photo2.zip
_______________________________________
## Step 6: Prepare for Next Batch

After compression:

mkdir /home/Local_address/photo

A new empty directory is created so image collection can continue.

Directory Structure

Before processing:

Local_address/

├── photo/

│   ├── image1.bmp

│   ├── image2.bmp

│   ├── ...

│   └── image108.bmp

└── zipphoto/

After processing:

Local_address/

├── photo/

└── zipphoto/

    ├── photo0.zip
    
    ├── photo1.zip
