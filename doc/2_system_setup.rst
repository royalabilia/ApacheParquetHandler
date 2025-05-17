===========
Set Up Your System
===========

Preparing things
-----------------------------
Clone **BruceProjectCode** (git clone git@github.com:royalabilia/BruceProjectCode.git)

Using vcpkg for build dependencies
-----------------------------
1. Clone vcpkg to BruceProjectCode\Code\Project\BruceProject (git clone https://github.com/Microsoft/vcpkg.git)
2. Download and install Apache Arrow and Boost using the vcpkg dependency manager
::
    cd vcpkg
    ./bootstrap-vcpkg.sh
    ./vcpkg integrate install
    ./vcpkg install boost:x64-windows arrow:x64-windows