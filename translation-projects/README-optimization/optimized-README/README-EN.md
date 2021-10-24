# perlporter

#### Description
Automated packaging tool for Perl modules.

Derived from cpanspec, perlporter helps to build perl modules into RPM packages automatically. It can be used to resolve the build dependencies of perl modules.

#### Installation
Run the following commands to install required software before using this tool:

1.  yum install cpan
2.  yum install perl

#### Preparation
Run the following commands to complete the system configuration:
1.  sudo cpan
2.  install Archive::Tar
3.  install Archive::Zip
4.  install Text::Autoformat
5.  install Parse::CPAN::Packages
#### Instructions

perlporter is a tool that can be used to create spec files and RPM packages for Perl modules.
For more details, use perlporter -h.

perlporter <package> -s -b -d -o python-<package>.spec

#### Contribution

1.  Fork the repository.
2.  Create a Feat_xxx branch.
3.  Commit your code.
4.  Create a pull request.

#### How to Create a RPM File (Using perl-XXX as an Example)

1.  Create a spec file:              perlporter --spec XXX
2.  Create a root path for RPM build:   perlporter --root XXX
3.  Build and Install RPM package: perlporter -B XXX
4.  Obtain more details:               perlporter -h


