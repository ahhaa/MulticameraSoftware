cmake_minimum_required(VERSION 2.8)
project( InitialFrameDetection )
INCLUDE ( /usr/share/cmake-3.5/Modules/FindPkgConfig.cmake )
find_package( OpenCV REQUIRED )
pkg_check_modules( REQUIRED flann )
find_package( OpenMP REQUIRED)
find_package( Boost REQUIRED COMPONENTS filesystem )
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS} -u MAIN__")
#SET(HAVE_F2C 1 CACHE BOOL "Do we have f2c or F77/I77?" )
#SET(LAPACKBLAS_DIR /usr/lib CACHE PATH "the name of the lapack library")
#SET(LAPACK_LIB lapack CACHE STRING "the name of the lapack library" )
#SET(BLAS_LIB blas CACHE STRING "the name of the blas library" )
#IF(HAVE_F2C)
#	SET(F2C_LIB f2c CACHE STRING " the name of the f2c library")
#ELSE(HAVE_F2C)
#	SET(F77_LIB libF77 CACHE STRING "the name of the F77 library" )
#	SET(I77_LIB libI77 CACHE STRING "the name of the I77 library" )
#ENDIF(HAVE_F2C)
add_executable( InitialFrameDetection Reconstruction3D_SIGGRAPH2012_robolounge.cpp
		DataUtility.cpp
		epnp.cpp
		MathUtility.cpp )
target_link_libraries( InitialFrameDetection 
	${OpenCV_LIBS}
	${Boost_FILESYSTEM_LIBRARY}
)
