##
## nmake file - to build in compiler console window for
##    microsoft compiler (cl) or compilers (like intel's icl)
##    which try to be mostly compatible (but better)
##
## this nmake file builds a static utilib 
##
## it expects to find a writeable utilib/src source directory at TOP
##
## (nmake libutilib.dll will make a shared library)
##
TOP=..\..

UTILIB=$(TOP)\src
STUDIES=$(TOP)\test\studies

INCLUDE_DIRS= /I . /I $(UTILIB)

RANLIB_LOC=$(UTILIB)\libs
ADT_LOC=$(UTILIB)\libs
MATH_LOC=$(UTILIB)\libs
CORE_LOC=$(UTILIB)\libs
IO_LOC=$(UTILIB)\libs
SYS_LOC=$(UTILIB)\libs
TYPEMNGR_LOC=$(UTILIB)\libs

CPPFLAGS=$(CPPFLAGS) /wd4244 /wd4996 /wd4530 /wd4552    # suppress warnings

all: libutilib.lib libutilib.dll

check: test_utilib.exe

help:
   @echo "nmake all" will build the library
   @echo "nmake clean" will delete all generated files
   @echo "nmake check" will build and run an executable
   @echo "nmake /?" lists all nmake options

RANLIB_C_SRC =        \
  $(RANLIB_LOC)\gencau.c   \
  $(RANLIB_LOC)\scauchy.c  \
  $(RANLIB_LOC)\genbet.c   \
  $(RANLIB_LOC)\genchi.c   \
  $(RANLIB_LOC)\genexp.c   \
  $(RANLIB_LOC)\genf.c     \
  $(RANLIB_LOC)\gengam.c   \
  $(RANLIB_LOC)\genmn.c    \
  $(RANLIB_LOC)\gennch.c   \
  $(RANLIB_LOC)\gennf.c    \
  $(RANLIB_LOC)\gennor.c   \
  $(RANLIB_LOC)\genunf.c   \
  $(RANLIB_LOC)\ignbin.c   \
  $(RANLIB_LOC)\ignpoi.c   \
  $(RANLIB_LOC)\sexpo.c    \
  $(RANLIB_LOC)\sgamma.c   \
  $(RANLIB_LOC)\snorm.c    \
  $(RANLIB_LOC)\genprm.c   \
  $(RANLIB_LOC)\global_rng.c \
  $(RANLIB_LOC)\ParkMiller.c 

RANLIB_CPP_SRC =        \
  $(RANLIB_LOC)\globals.cpp  \
  $(RANLIB_LOC)\LCG.cpp    \
  $(RANLIB_LOC)\PM_LCG.cpp 

RANLIB_OBJ = $(RANLIB_CPP_SRC:.cpp=.obj) $(RANLIB_C_SRC:.c=.obj)
RANLIB_SRC= $(RANLIB_C_SRC) $(RANLIB_CPP_SRC)

ADT_CPP_SRC =             \
  $(ADT_LOC)\CharString.cpp   \
  $(ADT_LOC)\BitArray.cpp     \
  $(ADT_LOC)\MixedIntVars.cpp \
  $(ADT_LOC)\lookupa.cpp      \
  $(ADT_LOC)\hash_fn.cpp      \
  $(ADT_LOC)\Factory.cpp      \
  $(ADT_LOC)\Ereal.cpp        

ADT_OBJ = $(ADT_CPP_SRC:.cpp=.obj)
ADT_SRC= $(ADT_CPP_SRC)

MATH_C_SRC =  $(MATH_LOC)\cov.c  $(MATH_LOC)\math.c

MATH_CPP_SRC =    \
  $(MATH_LOC)\median.cpp   \
  $(MATH_LOC)\cholesky.cpp \
  $(MATH_LOC)\math_basic.cpp 

MATH_OBJ = $(MATH_CPP_SRC:.cpp=.obj) $(MATH_C_SRC:.c=.obj)
MATH_SRC= $(MATH_C_SRC) $(MATH_CPP_SRC)

SYS_C_SRC = $(SYS_LOC)\misc.c           

SYS_CPP_SRC =  $(SYS_LOC)\seconds.cpp $(SYS_LOC)\memdebug.cpp     

SYS_OBJ = $(SYS_CPP_SRC:.cpp=.obj) $(SYS_C_SRC:.c=.obj)
SYS_SRC= $(SYS_C_SRC) $(SYS_CPP_SRC)

CORE_CPP_SRC = \
  $(CORE_LOC)\CommonIO.cpp     \
  $(CORE_LOC)\exception_mngr.cpp

CORE_OBJ = $(CORE_CPP_SRC:.cpp=.obj)
CORE_SRC = $(CORE_SRC)

IO_CPP_SRC = \
  $(IO_LOC)\comments.cpp     \
  $(IO_LOC)\mpiUtil.cpp      \
  $(IO_LOC)\logEvent.cpp     \
  $(IO_LOC)\nicePrint.cpp    \
  $(IO_LOC)\OptionParser.cpp    \
  $(IO_LOC)\TinyXML_helper.cpp    \
  $(IO_LOC)\Property.cpp \
  $(IO_LOC)\PropertyDict.cpp \
  $(IO_LOC)\Parameter.cpp \
  $(IO_LOC)\ParameterSet.cpp \
  $(IO_LOC)\ParameterList.cpp

IO_OBJ = $(IO_CPP_SRC:.cpp=.obj)
IO_SRC = $(IO_CPP_SRC)

TYPEMNGR_CPP_SRC = \
  $(TYPEMNGR_LOC)\Any.cpp      \
  $(TYPEMNGR_LOC)\PackBuf.cpp      \
  $(TYPEMNGR_LOC)\Serialize.cpp    \
  $(TYPEMNGR_LOC)\SerialStream.cpp \
  $(TYPEMNGR_LOC)\BinarySerialStream.cpp \
  $(TYPEMNGR_LOC)\fSerialStream.cpp \
  $(TYPEMNGR_LOC)\sSerialStream.cpp \
  $(TYPEMNGR_LOC)\MPIStream.cpp \
  $(TYPEMNGR_LOC)\XMLSerialStream.cpp \
  $(TYPEMNGR_LOC)\fXMLSerialStream.cpp \
  $(TYPEMNGR_LOC)\TypeManager.cpp

TYPEMNGR_OBJ = $(TYPEMNGR_CPP_SRC:.cpp=.obj)
TYPEMNGR_SRC = $(TYPEMNGR_CPP_SRC)

SOURCE_FILES= $(RANLIB_SRC) $(ADT_SRC) $(MATH_SRC) $(SYS_SRC) $(IO_SRC) $(CORE_SRC) $(TYPEMNGR_SRC)

OBJ_FILES= $(RANLIB_OBJ) $(ADT_OBJ) $(MATH_OBJ) $(SYS_OBJ) $(IO_OBJ) $(CORE_OBJ) $(TYPEMNGR_OBJ)

libutilib.lib: static/libutilib.lib

libutilib.dll: shared/libutilib.dll

static/libutilib.lib: headers $(OBJ_FILES)
    @if not exist static mkdir static
    lib /out:static/libutilib.lib /verbose $(OBJ_FILES)

shared/libutilib.dll: headers $(OBJ_FILES)
    @if not exist shared mkdir shared
    link /dll /out:shared/libutilib.dll /implib:shared/libutilib.lib $(OBJ_FILES)

headers:
    @if not exist utilib mkdir utilib  
    @copy utilib_config.txt utilib_config.h

{$(RANLIB_LOC)}.cpp.{$(RANLIB_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(RANLIB_LOC)}.c.{$(RANLIB_LOC)}.obj:
    $(CC) $(CFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.c

{$(ADT_LOC)}.cpp.{$(ADT_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(MATH_LOC)}.cpp.{$(MATH_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(MATH_LOC)}.c.{$(MATH_LOC)}.obj:
    $(CC) $(CFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.c

{$(SYS_LOC)}.cpp.{$(SYS_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(SYS_LOC)}.c.{$(SYS_LOC)}.obj:
    $(CC) $(CFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.c

{$(IO_LOC)}.cpp.{$(IO_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(CORE_LOC)}.cpp.{$(CORE_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

{$(TYPEMNGR_LOC)}.cpp.{$(TYPEMNGR_LOC)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp

clean:
        @-del /Q $(OBJ_FILES)
        @-del /Q static\*.lib
	@-rmdir static
        @-del /Q *.lib
        @-del /Q *.exe
        @-del /Q *.obj
        @-del /Q *.temp
        @-del /Q *.tmp
        @-del /Q iotest.*
        @-del /Q testfile
        @-del /Q utilib\*.h
	@-rmdir utilib

TEST_UTILIB_SRC= \
    $(STUDIES)\olist.cpp \
    $(STUDIES)\sort_test.cpp \
    $(STUDIES)\array.cpp \
    $(STUDIES)\bitarray.cpp \
    $(STUDIES)\multibitarray.cpp \
    $(STUDIES)\timing.cpp \
    $(STUDIES)\tuple.cpp \
    $(STUDIES)\iotest.cpp \
    $(STUDIES)\rngtest.cpp \
    $(STUDIES)\triang.cpp \
    $(STUDIES)\vectest.cpp \
    $(STUDIES)\stltest.cpp \
    $(STUDIES)\hash.cpp \
    $(STUDIES)\splay.cpp \
    $(STUDIES)\factory.cpp \
    $(STUDIES)\ereal.cpp \
    $(STUDIES)\heap.cpp \
    $(STUDIES)\calloc.cpp \
    $(STUDIES)\malloc.cpp \
    $(STUDIES)\pvector.cpp \
    $(STUDIES)\exception_test.cpp \
    $(STUDIES)\class_options.cpp \
    $(STUDIES)\option_parser.cpp \
    $(STUDIES)\sharedval.cpp \
    $(STUDIES)\any.cpp \
    $(STUDIES)\smartptr.cpp \
    $(STUDIES)\commonio.cpp \
    $(STUDIES)\stringtest.cpp \
    $(STUDIES)\listtest.cpp \
    $(STUDIES)\iotest_debug.cpp \
    $(STUDIES)\commonio_debug.cpp \
    $(STUDIES)\packbuf.cpp \
    $(STUDIES)\lphash.cpp \
    $(STUDIES)\hashedset.cpp \
    $(STUDIES)\matrix.cpp \
    $(STUDIES)\namespace.cpp \
    $(STUDIES)\qlist.cpp \
    $(STUDIES)\typeManager.cpp \
    $(STUDIES)\math.cpp \
    $(STUDIES)\sregistry.cpp \
    $(STUDIES)\paramTest.cpp \
    $(STUDIES)\serialize.cpp \
    $(STUDIES)\sserialstream.cpp \
    $(STUDIES)\fserialstream.cpp \
    $(STUDIES)\fserialstream-ref.cpp \
    $(STUDIES)\fxmlserialstream.cpp \
    $(STUDIES)\tests.cpp

TEST_UTILIB_OBJ = $(TEST_UTILIB_SRC:.cpp=.obj)

test_utilib.exe: headers $(TEST_UTILIB_OBJ)  libutilib.lib
   $(CPP) /Fe$@ $(TEST_UTILIB_OBJ)  static/libutilib.lib
   test_utilib.exe
   @if errorlevel 1 echo "FAIL"
   @if not errorlevel 1 echo "PASS"

{$(STUDIES)}.cpp.{$(STUDIES)}.obj:
    $(CPP) $(CPPFLAGS) $(INCLUDE_DIRS) /Fo$@ /c $*.cpp
