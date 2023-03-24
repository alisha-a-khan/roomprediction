# Technical Documentation for Embeddings.py
This code processes floor plan images to extract features and embeddings for use in machine learning models.

## Libraries
Several libraries are imported at the beginning of the code, including:

- Pandas: a library for data manipulation and analysis.
- PyTorch: a machine learning library that provides Tensors and dynamic computational graphs.
- OpenCV: a library for computer vision and image processing.
- NetworkX: a library for creating and manipulating graphs.
- Matplotlib: a library for creating data visualizations.
- Shapely: a library for working with geometric objects.
- Scikit-image: a collection of algorithms for image processing.
- In addition, the floortrans package is imported, which contains functions and classes for loading and manipulating floor plan images.

## Helper Functions
Several helper functions are defined in the code, including:

### `isolate_class`

This function takes an image of a floor plan and a target class as input and returns a binary mask with 1's at the locations where the target class is present in the image.

Inputs:
- `rooms` (numpy array): The input image of the floor plan.
- `CLASS` (int): The target class.

Outputs:
- `template` (numpy array): The binary mask with 1's at the locations where the target class is present in the input image.

Example:
```
import numpy as np

# Define an example input image
rooms = np.array([[1, 2, 2], [0, 2, 1], [2, 2, 1]])

# Call the function to isolate class 1
template = isolate_class(rooms, 1)

print(template)
```
Output of the example:
```
[[0 0 0]
 [0 0 1]
 [0 0 1]]
```
### `vis_nodes`
This function takes an image and a list of significant nodes (classes) as input and returns the contours of the rooms, the contours of the doors, and the centroid locations of the significant nodes. The function initializes empty lists to hold the room contours and nodes, gets a binary mask with 1's at the locations where the current class is present in the image, finds the contours of the connected components in the binary mask, adds each contour to the list of room contours, computes the centroid of the contour and adds it to the list of node locations. The function then returns the room contours, door contours, and node locations.
### `get_edges`
This function takes the contours of the rooms and doors as input and returns the connections between the rooms as a list of pairs of room indices and as a list of pairs of room centroid locations. The function initializes empty lists to hold the room connections as indices and as centroid locations, iterates over each room contour to compare with other room contours, checks if the polygons intersect and if there is a door between the two rooms, and adds the pair of room indices or room centroids to the appropriate list if the conditions are met. The function then returns the list of connections as indices and as centroid locations.

## Main Function
The `process_file` function is the main function that takes a file path as input and returns embeddings, embeddings2, and Y.

The function loads a file containing a dictionary of floor plan images and iterates over each floor plan in the data. For each floor plan, it extracts the contours of the rooms, doors, and nodes and computes several features, including the relative areas of the rooms, the number of adjacent rooms, and the average area of each room type.

The node classes are converted to one-hot vectors and concatenated with the relative areas to create the input feature matrix X. The adjacency matrix A is computed from the edges of the graph, and the node embeddings are computed using the adjacency matrix and node attributes.

The embeddings, embeddings2, and Y are concatenated into a pandas dataframe and returned. The `X_all` variable is also returned, which can be used for the non-graph model.

Example:
```
X_train, Y_train, df_train, X_all_train=process_file("/dataframes/train.pkl")
```


## Conclusion
This code provides a method for extracting features and embeddings from floor plan images using graph neural networks. The code can be used as a basis for developing machine learning models for floor plan analysis and generation.

