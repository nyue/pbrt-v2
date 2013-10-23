FIND_PACKAGE ( Bison )
FIND_PACKAGE ( Flex )

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

ADD_DEFINITIONS ( -DPBRT_HAS_OPENEXR )

INCLUDE_DIRECTORIES (
  .
  )

ADD_LIBRARY ( pbrt STATIC
  # Potentially to be generated LEX and YACC parser files
  core/pbrtlex.cpp
  core/pbrtparse.cpp
  ${LIB_CSRS}
  ${LIB_CSSSRCS}
  )
