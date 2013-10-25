FIND_PACKAGE ( Bison )
FIND_PACKAGE ( Flex )
FIND_PACKAGE ( OpenEXR )
FIND_PACKAGE ( ILMBase )

# LIB_CSRCS=core/targa.c
# LIB_CXXSRCS  = $(wildcard core/*.cpp) core/pbrtlex.cpp core/pbrtparse.cpp
# LIB_CXXSRCS += $(wildcard accelerators/*.cpp cameras/*.cpp film/*.cpp filters/*.cpp )
# LIB_CXXSRCS += $(wildcard integrators/*.cpp lights/*.cpp materials/*.cpp renderers/*.cpp )
# LIB_CXXSRCS += $(wildcard samplers/*.cpp shapes/*.cpp textures/*.cpp volumes/*.cpp)
FILE (GLOB LIBCSRCS core/*.c )
FILE (GLOB LIBCXXSRCS
  core/*.cpp accelerators/*.cpp cameras/*.cpp film/*.cpp filters/*.cpp
  integrators/*.cpp lights/*.cpp materials/*.cpp renderers/*.cpp
  samplers/*.cpp shapes/*.cpp textures/*.cpp volumes/*.cpp
)
# MESSAGE ( "LIBCSRCS ${LIBCSRCS}" )
# MESSAGE ( "LIBCXXSRCS ${LIBCXXSRCS}" )

ADD_DEFINITIONS ( -DPBRT_HAS_OPENEXR -DPBRT_PROBES_NONE )

INCLUDE_DIRECTORIES (
  .
  core
  ${ILMBASE_INCLUDE_DIRS}
  ${OPENEXR_INCLUDE_DIRS}
  )

ADD_LIBRARY ( pbrt STATIC
  # Potentially to be generated LEX and YACC parser files
  core/pbrtlex.cpp
  core/pbrtparse.cpp
  ${LIBCSRCS}
  ${LIBCXXSRCS}
  )

# ADD_EXECUTABLE ( bsdftest )
# ADD_EXECUTABLE ( exravg )
# ADD_EXECUTABLE ( exrdiff )
# ADD_EXECUTABLE ( exrtotiff )
ADD_EXECUTABLE ( pbrt_exe
  main/pbrt.cpp
  )
SET_TARGET_PROPERTIES ( pbrt_exe
  PROPERTIES
  OUTPUT_NAME
  pbrt
  )

TARGET_LINK_LIBRARIES ( pbrt_exe
  pbrt
  ${Ilmbase_HALF_LIBRARY}
  ${Ilmbase_IEX_LIBRARY}
  ${Ilmbase_ILMTHREAD_LIBRARY}
  ${Ilmbase_IMATH_LIBRARY}
  ${Openexr_ILMIMF_LIBRARY}
  )
