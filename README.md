# VLASS-cutout-URL-generator

## Jupyter Notebook to obtain VLASS cutouts 
### By G. R. Sivakoff (University of Alberta); B. Sebastian, (University of Manitoba)

The provided Python code automates the process of retrieving URLs for VLASS quick look image fits files for 3' X 3' boxes centred on a set of sky coordinates. The code reads a catalog with coordinates from a CSV file, each represented by columns RA and DEC. For each coordinate, it fetches the corresponding VLASS image URL through the <b><em>getCadcVlassUrl()</em></b> function. These URLs are stored in a new column within the dataset. The augmented data, now including URLs for VLASS images, is finally saved back to a CSV file for further use and analysis.

* <font color=maroon><b> Specify the catalog input. </b></font><br>
Download the csv version of an entire catalog (e.g.,
<em>CIRADA_VLASS1QLv3.1_table1_components.csv</em>, <em>CIRADA_VLASS2QLv2_table1_components.csv</em>, or
<em>CIRADA_VLASS2SEv2_table1_components.csv</em>) and make a subset of the entire catalog. 
Specify the location of the catalog in Cell 2 of this notebook. 
This code assumes the python code is being run in the same directory as the downloaded file.
 
* <font color=maroon><b>Input the correct epoch and the imagetype.</b></font><br>
In this notebook, we extract URLs for the 'Epoch 1 Quick Look' images. Alternative options are commented next to the parameters in Cell 2.
* <font color=maroon><b>Comment out "testRunFlag = True" in Cell 2 if you want to retrieve the CADC URLs for the entire catalog.</b></font><br>
If the variable <em>testRunFlag</em> is "True", only the first five rows will be affected; if the variable is "False", the code operates on the entire catalog. This variable is extremely useful for testing the code before running on a large CSV file.   
* <font color=maroon><b>This code does not produce URLs for mosaiced images.</b></font><br>
In the case that there are multiple cutout images appropriate for a source in your query, only the final URL from the list of URLS for that source will be returned. This URL should be for the latest (by observation date) image.
* <font color=maroon><b>Some tests of this took 5 seconds per source! Check back to see if we develop speedier methods.</b></font><br>


### Note:

The code snippets here are based off code that are helping add VLASS Quicklook RMS Functionality and Single Epoch Functionality to the CIRADA cutout service. These are only meant to be examples and they may need to be written with more proper coding principles, upgraded for working with Python versions > 3.7, have more extensive unit testing performed, and undergo optimization refactoring.

Nevertheless, some users may find these useful if they do not want to use a Dockerized version of the CIRADA command-line cutout service or the online CIRADA cutout service. Please note that CIRADA is also looking to implement an API for the online service that would include full access to all surveys in the CIRADA cutout services.



### Code Setup

Please use this cell to edit important variables for this notebook.

* The variable <em>onColab</em> ensures astroquery is installed when Google Colab runs this code.
* The variable <em>testRunFlag</em> allows the code to only operate on the first 5 sources in a catalog for testing purposes.
* The variable <em>radius</em> sets the size of the square image to be extracted.
* The array <em>epoch</em> sets the epochs to be considered, although onbly the latest epoch for a source will be output.
* The array <em>imageType</em> sets the type of image to be output. Please note this example code that outputs to a single column per source for a catalog works correctly only when one <em>imageType</em> is specified.
