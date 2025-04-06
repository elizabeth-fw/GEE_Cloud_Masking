# GEE_compositing

AOI
  -	Import AOI shapefile from assets.
    
Scaling factors
  -	Apply optical and thermal scaling factors for surface reflectance imagery.
  -	Imagery scaling factors can be found on the Earth Engine Data Catalog.

Masking
  -	Cloud masking based on the different QA bands. 
  -	Filter out pixels flagged as cloudy, shadowed etc. and only keep clean pixels indicating no cloud.   
  -	Apply a buffer to get rid of the clouds surrounding the QA mask. 
  -	Manually compute cloud score. 
  -	Apply a strong buffer and shadow mask to the cloud score masking. 
  -	Detect possible shadow areas and calculate shadow azimuth based on solar azimuth angle. 
  -	Map cloud shadow projection onto dark pixel areas. 
  -	Buffer cloud and shadow mask. 

Image collection & compositing 
  -	Build a cloud-filtered, scaled image collection for a chosen time period. 
  -	Compute composites for each year with various levels of masking. 
  -	Add layers to the map for each year for visualization (optional – used t check cloud masking performance). 

Image mosaicking 
  -	Create a mosaic by stacking the composites in an image collection and apply the mosaic operation 

Image export 
  -	Specify the region to export and increase max pixel count if needed. 


For Sentinel 2 only:
Buffer Cloud Probability Mask
  -	Since the additional CLOUDY_PIXEL_PERCENTAGE filter, is not usable metadata in GEE's S2 Cloud Probability band (S2_CloudProb),      the two collections, S2_Harmonized and S2_CloudProb, must be manually aligned.
  -	This 'matching' is done by filtering through the times that the S2_Harmonized images are taken to match them each with the time     that the corresponding derived 'Cloud Probability' image was produced.
  -	There is a small difference in time between when these two events (when the S2_Harmonized and the S2_CloudProb images are           produced) occur.
  -	Hence, the getCloudProbImage function below adds a buffer of an hour before and after the harmonized images were produced to   
    match to then filter the could probability images.
  -	Function will be mapped to S2_Harmonized collection to create corresponding S2_CloudProb collection. 
  -	Create a cloud probability mask (where cloud probability is less than 20%).
  -	Apply the cloud probability mask to the Sentinel-2 image.


