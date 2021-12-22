1. ==========
   geo-coding
   ==========
   geo-coding is a Python client for geo-coordinate-related services, including common and popular features such as geocoder, coordinate calculation, and coordinate system conversion.

   Use Cases
   ------------

   * Used for businesses and projects that require latitude and longitude geographic coordinate positioning and calculation, such as various geographic coordinate big data projects.
   * Used as the underlying toolkit for similar map projects, providing tools for many businesses that need to calculate latitude and longitude to determine orientation.

   Features
   ------------
   1. Geocoder: Enable developers to easily locate coordinates of addresses, cities, countries, and landmarks around the world using third-party geocoding programs and other data sources.
      Plan development sequence: Baidu, Gaode...

   2. Coordinate system conversion: Convert latitude and longitude coordinates using the standard of Baidu, Gaode, Geodetic Coordinate System, and Ordnance Survey...

   3. Distance: calculate the actual distance between coordinates and other practical functions.

   4. Unit conversion.

   5. Data: Longitude and Latitude Coordinates of China's Border

   Advantages
   ------------
   At present, most of the software with geographic functions is very bloated, and there are only few coordinate software adapted to Map of China. The library is a lightweight tool based on only Python, which aimed to enrich the functions and provide low-level and fast services for actual business.

   Development Plan Sequence
   ------------
   * 2,5,3,4,1

   Version Support
   ------------
   * Python 3.x
   * Linux: build/passing
   * Windows: build/passing

   Usage examples
   ------------
   *


   Start Contributing
   ------------
   Ready to contribute or use? Here's how to set up "geo-coding" for local development.

   1. Fork `geo-coding` repository on Gitee.
   2. Clone your repository locally:::

        $ git clone https://gitee.com/weihaitong/geo-coding.git

   3. Here is how to use this tool:::

        $ cd geo-coding/
        $ python setup.py install

   4.If you want to contribute to the project, you can create a branch for local development.::

        $ git checkout -b name-of-your-bugfix-or-feature
       
       Now you can make changes locally.

   5. Submit your changes and push your branch to Gitee:::

        $ git add .
        $ git commit -m "Your detailed description of the changes"
        $ git push origin name-of-your-bugfix-or-feature

   6. Submit a pull request on Gitee.


   Pull Request Guide
   -----------------------

   Please check that it meets the following guidelines before submitting a pull request:

   1. The pull request should include tests.
   2. Update the document if the pull request adds a feature. Put your new feature into a function with a document string and add it to the list in README.rst.
   3. The pull request should work with Python 3.x. And make sure the tests pass all supported Python versions.
