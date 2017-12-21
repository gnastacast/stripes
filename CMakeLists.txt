cmake_minimum_required (VERSION 2.8)

set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)
set(CMAKE_DISABLE_SOURCE_CHANGES  ON)

if ("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_BINARY_DIR}")
  message(SEND_ERROR "In-source builds are not allowed.")
endif ()

project (stripe)

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLEW REQUIRED)

set (CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

find_package(SuiteSparse REQUIRED)
include_directories(include
					src
					${OPENGL_INCLUDE_DIR}
					${GLUT_INCLUDE_DIRS}
					${GLEW_INCLUDE_DIRS}
					${SUITESPARSE_INCLUDE_DIRS})

SET(CMAKE_CXX_FLAGS "-DSP_COMPILE_COMMAND_LINE -O3 -Wall -Wno-deprecated -Werror -pedantic")

add_executable(stripe
		src/main.cpp
		src/Camera.cpp 
		src/Complex.cpp
		src/DenseMatrix.cpp
		src/Edge.cpp
		src/Face.cpp
		src/HalfEdge.cpp
		src/Image.cpp
		src/LinearContext.cpp
		src/LinearEquation.cpp
		src/LinearPolynomial.cpp
		src/LinearSystem.cpp
		src/Mesh.cpp
		src/MeshIO.cpp
		src/Quaternion.cpp
		src/Real.cpp
		src/Shader.cpp
		src/SparseMatrix.cpp
		src/Variable.cpp
		src/Vector.cpp
		src/Vertex.cpp
		src/Viewer.cpp)

target_link_libraries( stripe
						${OPENGL_LIBRARIES}
						${GLUT_LIBRARIES}
						${GLEW_LIBRARIES}
						${SUITESPARSE_LIBRARIES})