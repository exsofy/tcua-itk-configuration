# Use xerces with codefull customization

xerces shared library is distributed and used by Teamcenter server
installation. The header files are not distributed by foundation installation
but available in soa_client package.

## Install header files
Header files are avaiable in soa_client package distributed with Teamcenter
Install the soa_client package, if not allready done.


## Configure build
Add `-I$(SOA_CLIENT_KIT)\toolbox\XMLTools\include` include to CPP_INCLUDES
in makefile.wntx64

e.g.
```make
CPP_INCLUDES       = -I$(SOA_CLIENT_KIT)\cpp\includes\cpp\include -I$(SOA_CLIENT_KIT)\toolbox\XMLTools\include -I$(SOA_CLIENT_KIT)\toolbox\XMLTools\include\icu\common
```

Add xerces314 to YOURLIBRARY_LIBS in makefile

e.g.
```make
YOURLIBRARY_LIBS   = $(LIB_PREFIX)metaframework$(LIB_SUFFIX) \
                                  ...
                                  $(LIB_PREFIX)mld$(LIB_SUFFIX)  $(LIB_PREFIX)base_utils$(LIB_SUFFIX) $(SYSLIBS) \
                                  xerces314$(LIB_SUFFIX)
                                  ```

## Configure BMIDE \(eclipse CDT\)
Let CDT know where the xerces headers are. Add your include path to
Project(RMB)->Properties->C/C++ General->Paths ans Symbols->Includes->GNU C++

e.g.
`C:\plm\tc112\soa_client\toolbox\xml4c\include`


## Use xerces
If the configuration works, xercesc shall be normally used

e.g.
```C++
#include <xercesc/util/PlatformUtils.hpp>
#include <stdlib.h>
#include <string.h>
#if defined(XERCES_NEW_IOSTREAMS)
#include <iostream>
#else
#include <iostream.h>
#endif
#include <xercesc/parsers/SAXParser.hpp>
#include <xercesc/sax/HandlerBase.hpp>

#include <xercesc/sax/AttributeList.hpp>
#include <xercesc/sax/SAXParseException.hpp>
#include <xercesc/sax/SAXException.hpp>
#include <xercesc/framework/MemBufInputSource.hpp>

XERCES_CPP_NAMESPACE_USE
```
