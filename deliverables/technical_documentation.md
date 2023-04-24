# Technical Documentation

## Dataset Overview

The Cubicasa 5k dataset is a large-scale dataset of floorplans that contains 5,000 floorplans from various building types, such as apartments, houses, and offices.

What makes this dataset particularly useful is the fact that the floorplans are not only annotated with room type labels, such as bedroom, kitchen, living room, etc., but also with icon labels, such as electrical appliance, sauna, closet, etc. This makes it a valuable resource for training and evaluating room type classification models.

For each floorplan in the dataset, there are two corresponding  2D numpy arrays (images), one for the room layer and one for the icon layer. Both arrays are of the same size and contain numerical values that represent the room type or icon label for each pixel in the floorplan.

![rooms](images/Screen_Shot_2023-04-24_at_2.08.47 AM.png)
