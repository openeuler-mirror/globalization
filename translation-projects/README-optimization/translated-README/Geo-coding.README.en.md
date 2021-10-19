==========
Geo-coding
==========
Geo-coding is a Python client for geographic coordinate-related services, including common and popular geocoding, coordinate calculation, and coordinate system conversion functions.

Service Scenario
------------

* Serving for services and projects that require latitude and longitude geographic coordinate positioning and calculation, such as various geographic coordinate big data projects.
* Serving for the underlying toolkit that serves similar map projects, and providing tools for many businesses that need to calculate latitude and longitude to determine orientation.

Function
------------
1. Geocoder: Enable developers to use third-party geocoding programs and other data sources to easily locate the coordinates of addresses, cities, countries, and landmarks around the world. Development sequence: Baidu, Gaode...
   
2. Coordinate system conversion: For example, Baidu, Gaode, Geodetic Coordinate System and National Bureau of Survey and Measurement and other standards perform longitude and latitude coordinate conversion.

3. Distance: Calculate the actual distance between coordinates and other practical functions.

4. Unit conversion

5. Data: Longitude and Latitude Coordinates of China's Border

Advantage
------------
Nowadays, most of the software with geographic functions are complicated, and there are not many coordinate softwares that adapt to Chinese maps. The library is a lightweight tool for pure Python libraries,aiming at more functions and providing low-level fast services for actual business.

Development Plan Sequence
------------
* 2,5,3,4,1

Version
------------
* Python 3.x
* Linux: build/passing
* Windows: build/passing

Example of Use
------------
*


How to Contribute
------------
Are you ready to contribute or use? This is how to set up "geocoding" for local development.

1. Fork the `geo-coding` repository on Gitee.

2. Clone your repository locally:

     $ git clone https://gitee.com/weihaitong/geo-coding.git

3. This is how you use this tool:

     $ cd geo-coding/
     $ python setup.py install

4. If you want to contribute to this project, you can create a branch for local development:

     ```shell
     $ git checkout -b name-of-your-bugfix-or-feature
     #Now You can now make changes locally.
     ```

5. Submit your changes and push your branch to Gitee:

     ```shell
     $ git add .
     $ git commit -m "your description"
     $ git push origin name-of-your-bugfix-or-feature
     ```

6. Submit a pull request through the Gitee website.


Pull Request Guidelines
-----------------------

Before submitting a pull request, please check that it meets the following guidelines:

1. The pull request should include testing.
2. If the pull request adds a function, the documentation should be updated. Put your new function in a function with a docstring and add the function to the list of README.rst.
3. The pull request should apply to Python 3.x. And make sure that the test passes all supported Python versions.