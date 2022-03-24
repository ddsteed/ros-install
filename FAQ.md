# noetic

## General


## Linux
## MAC
+ log4cxx

	> no viable conversion from normal pointer to smart shared_ptr
  
   - log4cxx 0.12.0 upgrade pointer to smart one, so one has to install 0.10.0 version and link it manually. (do NOT use brew version.)
   - brew uninstall default log4cxx since catkin\_make's find_package will search system firstly.
   
+ qt\_gui\_cpp

	> Failed to find "gl.h"
	
	- xcode changes OpenGL directory 
	- ln -s "$(xcrun --sdk macosx --show-sdk-path)/System/Library/Frameworks/OpenGL.framework/Headers" \
  		/usr/local/include/OpenGL
  -  export CMAKE_PREFIX_PATH="/usr/local/include/OpenGL:$CMAKE\_PREFIX\_PATH"
	
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
	
	- close all warning messages since ROS is compiled by non-ISO C++-11
	- add CXXFLAGS="-w" 