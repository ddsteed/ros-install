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
   - brew uninstall default log4cxx since catkin\_make's find_package will search system firstly
   - install log4cxx 0.10.0 from source
   
+ qt\_gui\_cpp

	> Failed to find "gl.h"
	
	xcode changes OpenGL directory 

	```bash
	ln -s "$(xcrun --sdk macosx --show-sdk-path)/System/Library/Frameworks/OpenGL.framework/Headers"  /usr/local/include/OpenGL	
	export CMAKE_PREFIX_PATH="/usr/local/include/OpenGL:$CMAKE_PREFIX_PATH"
  	```
    
+ rviz

	>  Could NOT find OpenGL (missing: OPENGL\_gl\_LIBRARY)
	
	- set OPENGL\_gl\_LIBRARY manually

		+ in set\_env function:

		```bash
	  export OPENGL_gl_LIBRARY="$(xcrun --sdk macosx --show-sdk-path)/System/Library/Frameworks/OpenGL.framework/Versions/Current/Libraries"
	  ```

	   + in catkin\_make\_comp function, add cmake args: 
	   
	  	```bash
	  	-DOPENGL_gl_LIBRARY=$OPEN_gl_LIBRARY
	  	```

	+ vision\_opencv/cv_bridge

	> /usr/local/include/boost/predef/library/std/cxx.h:38:5: error: function-like macro 'BOOST\_PREDEF\_MAKE\_10\_VVPPP' is not defined

	"make.h" defines BOOST\_PREDEF\_MAKE\_10\_VVPPP macro which is defined by "version.h" while "cxx.h" does NOT include correctly.
	
	- In "cxx.h", add
	
		```cpp
		 #define BOOST_VERSION_NUMBER(major,minor,patch) \
		   	 ( (((major)%100)*10000000) + (((minor)%100)*100000) + ((patch)%100000) )
	   	 
	   	 #define BOOST_PREDEF_MAKE_10_VVPPP(V)  BOOST_VERSION_NUMBER(((V)/1000)%100,0,(V)%1000)
  		```

# foxy
## General

+ git

	> git download fails

	- find a VPN proxy. 
	- use git ssh instead of git http in "~/.gitconfig"
		
## Linux

+ library_abs 

	> library_abs NOTFOUND under Linux
   
	- 

	```bash
   apt install foxy_desktop
   ```
+ qt\_gui\_cpp

	> ModuleNotFoundError: No module named 'sipconfig'
	
	SIP v5 will not include an extensible build system, i.e it will not provide an equivalent of SIP v4’s sipconfig module. Consequently a version of PyQt built with SIP v5 will not provide an equivalent of the pyqtconfig module.
	
	However, this error does NOT occur in MAC.
	
	- install sip 4.19 from source
	- install sip 4.19 through conda

## MAC
+ qt\_gui\_cpp

	> CMake Warning at /opt/ros/foxy\_src/install/python\_qt\_binding/share/python\_qt\_binding/cmake/sip\_helper.cmake:27 (message):
	
  	> SIP binding generator NOT available.
Call Stack (most recent call first):
  src/qt\_gui\_cpp\_sip/CMakeLists.txt:56 (include)

	> Python binding generators:
CMake Error at src/CMakeLists.txt:10 (message):
  No Python binding generator found.
  
  - removed the error in ros-visualization/qt\_gui\_core/qt\_gui\_cpp/src/CMakeLists.txt:

		```cpp
		message(STATUS "Python binding generators: ${qt_gui_cpp_BINDINGS}")
		if(NOT qt_gui_cpp_BINDINGS)
		  # message(FATAL_ERROR "No Python binding generator found.")
		endif()
		```

+ rcpputils

	> gtest-matchers.h:739:3: error: definition of implicit copy constructor for 'MatchesRegexMatcher' is deprecated because it has a user-declared copy assignment operator [-Werror,-Wdeprecated-copy]
	
	close all warning messages since ROS is compiled by non-ISO C++-11
	- add 

	```bash
	CXXFLAGS="-w" 
	```