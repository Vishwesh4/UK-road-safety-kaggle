# UK-road-safety-kaggle
In the data set which has been taken from kaggle competition [UK Road Safety: Traffic Accidents and Vehicles](https://www.kaggle.com/tsiaras/uk-road-safety-accidents-and-vehicles), Accident_information.csv has been considered. The following csv file contains many information about the accident event that has occured in the period of 2005-2007. Out of the many columns, latitude and longitude is also given. Using Geopandas and maps taken from google earth, I have tried to make a heat map of the accidents. Since giving just latitude and longitude is non informative. I have written a code to link the accident events to the geographical road map, in particular number of casualities/accidents that happened in each and every road of multiple cities of UK in particular London, Manchester, Birmingham. This code with the tabular road wise data, also gives a nice heat map. Further, this code can be used to analyze any section of UK given geographical road data which can be extracted from google earth/map.
## Methodology
###Data collection
1. Since we are dealing with latitude and longitude values, we work with Geopandas. Also since these points represent accidents we also need to collect the road data of England
2. In order to plot these points, I had to download from internet the road map of England. It is stored in `./Great Britain/roads.shp`.
3. Next we need to extract only those roads which are limited to a city. From google earth, we can extract geographical polygons, which define the limits of a region. We now need to extract its road map.
4. We are considering 3 main cities for our analysis namely London, Manchester, Birmingham. In order to get their road map we needed to extract boundary of city from Google Earth and take Intersection of the road map which was done using geopandas. Note that since road map of full England is available, we can take any boundary from Google earth and get its road map using intersection of the boundary with road map of England.

###Algorithm
1. Now that the road data is available, we have to link the latitude, longitude from Accident_information.csv to the roads of a certain city. 
2. Since the points exactly did not lie on the road data, which are represented as lines in geopandas. I applied a neighbour search algorithm. Since searching across whole road data was not viable, I made a region across each query point and search the roads which had their min/max lat/lon in that search region. This search led to decrease from 82 hrs to 2hrs of computation time
3. In order to calculate casualty per meter, I did a Mercator projection of lat/lon in order to calculate distance in meters. The previous distance was a simple euclidean distance.  Using Geopandas I found the length of each road and using this information successfully got the desired feature Casualty per meter.


## Results
The images is best viewed in a image viewer because of its fine resolution.
- <ins>UK severity map</ins>   
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/UK_severity.png)  

- <ins>Tables of london roads</ins>  
Ordered in descending order of casualities 
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/Table1.png) 
Ordered in descending order of casulaity per meter  
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/Table2.png)  

- <ins>London road heat map</ins>  
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/london_road.png) 

- <ins>Manchester road heat map</ins>  
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/manchester_road.png) 

- <ins>Birmingham road heat map</ins>  
![Alttext](https://github.com/Vishwesh4/UK-road-safety-kaggle/master/images/Birmingham_roads.png)  

## Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites
The following notebook is written on google colab, hence all the required libraries are installed in the first cell itself. However to run it locally, the following libraries are required.
Libraries needed

```
geopandas
shapely
seaborn
pandas
```
### Dataset
* `Accident_Information.csv`- Can be downloaded from the kaggle competition link given at the top
* `England and cities road map`- Since google colab is used, you can replicate the [given folder in drive ](https://drive.google.com/drive/folders/1v9lg_PbJVALelHHF5OYZ3cVTixlKVdj2?usp=sharing) to your own google drive account. This drive can be now directly used by the google colab file `contour_generation.ipynb`.