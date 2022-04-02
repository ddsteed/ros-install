# noetic

## General
+ Visualization_msg/Marker.h

	> Marker.h NOT found
	
	Some package is compiled based on others, however, parallelized compilations do NOT have fixed order so it may occur library file not found.
	
	- run compilation again :-)
	

## Linux
+ 

## MAC

+ general

	> mach-o file, but is an incompatible architecture (have 'arm64', need 'x86_64')
	
	M1 chip compiles code as arm64 architecture. One has to add 'arch -x86_64' before 'make' or 'CC/CXX'.
	  
+ kdl_parser

	> Project 'kdl\_parser' tried to find library
  '$<$<NOT:$<CONFIG:Debug>>:/usr/local/lib/liburdfdom\_sensor.dylib>'.
  
  	- install urdfdom from source.
  	
  	
+ log4cxx

	> no viable conversion from normal pointer to smart shared_ptr
  
   log4cxx 0.12.0 upgrade pointer to smart one, so one has to install 0.10.0 version and link it manually. (do NOT use brew version.)
   - brew uninstall default log4cxx since catkin\_make's find_package will search system firstly.
   
+ qt\_gui\_cpp

	> Failed to find "gl.h"
	
	xcode changes OpenGL directory 
	- ln -s "$(xcrun --sdk macosx --show-sdk-path)/System/Library/Frameworks/OpenGL.framework/Headers"  /usr/local/include/OpenGL
  	- export CMAKE\_PREFIX\_PATH="/usr/local/include/OpenGL:$CMAKE\_PREFIX\_PATH"
    
+ rviz

	>  Could NOT find OpenGL (missing: OPENGL\_gl\_LIBRARY)
	
	- set OPENGL\_gl\_LIBRARY manually
	
	  + export OPENGL\_gl\_LIBRARY="$(xcrun --sdk macosx --show-sdk-path)/System/Library/Frameworks/OpenGL.framework/Versions/Current/Libraries"
	  + cmake args: -DOPENGL\_gl\_LIBRARY=$OPEN\_gl\_LIBRARY

	+ vision\_opencv/cv_bridge

	> /usr/local/include/boost/predef/library/std/cxx.h:38:5: error: function-like macro 'BOOST\_PREDEF\_MAKE\_10\_VVPPP' is not defined

	"make.h" defines BOOST\_PREDEF\_MAKE\_10\_VVPPP macro which is defined by "version.h" while "cxx.h" does NOT include correctly.
	
	In "cxx.h", add
	
	- \#define BOOST\_VERSION\_NUMBER(major,minor,patch) \\
    ( (((major)%100)*10000000) + (((minor)%100)*100000) + ((patch)%100000) )
    
   - \#define BOOST\_PREDEF\_MAKE\_10\_VVPPP(V) BOOST\_VERSION\_NUMBER(((V)/1000)%100,0,(V)%1000)

	
# foxy
## General

+ git

	> git download fails

	- find a VPN proxy. 
	- use git ssh instead of git http in "~/.gitconfig"
		
## Linux

+ library_abs 

	> library_abs NOTFOUND under Linux
   
   - apt install foxy_desktop


## MAC
+ rcpputils

	> gtest-matchers.h:739:3: error: definition of implicit copy constructor for 'MatchesRegexMatcher' is deprecated because it has a user-declared copy assignment operator [-Werror,-Wdeprecated-copy]
	
	close all warning messages since ROS is compiled by non-ISO C++-11
	- add CXXFLAGS="-w" 