# RubyPorter

#### Description
This is an RPM packager bot for Ruby modules from [rubygems.org](rubygems.org). This bot allows you to create **spec** files and create RPM for Ruby modules.

#### Preparation

Install the following software before using the RubyPorter.

*  GCC 
*  GDB 
*  libstdc++-devel 
*  ruby-devel
*  rubygems-devel

#### Installation

Run **python3 setup.py install** to install.

#### Instructions
1. Run **rubyporter -s xxx** to create a **spec** file named ***xxx***, note that this should be an existed tool in the RubyGems package. Run **-o *yyy*** to save the specification log to the ***yyy*** file.
```
e.g.  rubyporter -s puma (generate and display the spec log on the screen)
     
      rubyporter -s puma -o rubygem-puma.spec (generate and save the spec log to rubygem-puma.spec)
```


2. Build an RPM package in the name ***rubyporter -b xxx***.

3. Build and Install the RPM package, ***rubyporter -B xxx***.

4. For more details, please use ***rubyporter -h***.

#### Contribution
1.  Fork the repository.
2.  Create a **Feat_xxx** branch.
3.  Commit your code.
4.  Create a pull request.