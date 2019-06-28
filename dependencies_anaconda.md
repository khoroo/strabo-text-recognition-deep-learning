Dependencies to conda install for running strabo:

tensorflow
opencv
shapely
pillow
flask
matplotlib
plumbum
tesserocr 

With channels 

-c mcs07 conda-forge 

(Some packages are not maintained in the main conda, but a 3rd party source)

Full command:

conda install -c mcs07 -c conda-forge tensorflow opencv shapely pillow flask matplotlib plumbum tesserocr
