# noetic
## Linux
## MAC
1. log4cxx: no viable conversion from normal pointer to smart shared_ptr
  
   A: log4cxx 0.12.0 upgrade pointer to smart one, so one has to install 0.10.0 version and link it manually. (do NOT use brew version.)

# foxy
## Linux
### library

1. library_abs NOTFOUND under Linux
   
   A: apt install foxy_desktop


## MAC
1. git download fails

	A: 1) find a VPN proxy. 
		2) use git ssh instead of git http in "~/.gitconfig"
		