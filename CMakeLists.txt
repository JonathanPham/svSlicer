cmake_minimum_required(VERSION 2.6) # todo: I can probably change the required cmake version here

set(CMAKE_CXX_STANDARD 17) # https://stackoverflow.com/a/55362633

project(svslicer) # change "svslicer" to whatever project and output executable file name that I want. Make sure to change svslicer everywhere in this file

include_directories($ENV{EIGEN_DIR}) # https://stackoverflow.com/questions/51443374/use-environment-variable-to-set-include-directories

find_package(VTK COMPONENTS # this packages are copied from https://kitware.github.io/vtk-examples/site/Cxx/PolyData/CellCentersDemo/ ; need to change the packages used if I develop a C++ code that uses some other VTK functions, e.g., the BooleanOperationPolyDataFilter.cxx code in https://kitware.github.io/vtk-examples/site/Cxx/PolyData/BooleanOperationPolyDataFilter/ uses different VTK functions
    CommonColor
    CommonCore
    CommonDataModel
    FiltersCore
    FiltersExtraction
    FiltersGeometry
    FiltersModeling
    FiltersSources
    IOGeometry
    IOLegacy
    IOPLY
    IOXML
    InteractionStyle
    RenderingContextOpenGL2
    RenderingCore
    RenderingFreeType
    RenderingGL2PSOpenGL2
    RenderingOpenGL2
)

include(${VTK_USE_FILE})

add_executable(svslicer src/main.cpp)

target_link_libraries(svslicer ${VTK_LIBRARIES})

# vtk_module_autoinit is needed
vtk_module_autoinit( # this is needed for some reason, but I am not sure why
    TARGETS svslicer
    MODULES ${VTK_LIBRARIES}
)