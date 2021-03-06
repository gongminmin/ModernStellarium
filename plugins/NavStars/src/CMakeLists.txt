INCLUDE_DIRECTORIES(
     .
     gui
     ${CMAKE_BINARY_DIR}/plugins/NavStars/src
     ${CMAKE_BINARY_DIR}/plugins/NavStars/src/gui
)

LINK_DIRECTORIES(${BUILD_DIR}/src)

SET(NavStars_SRCS
     NavStars.hpp
     NavStars.cpp
     gui/NavStarsWindow.hpp
     gui/NavStarsWindow.cpp
)

SET(NavStars_UIS
     gui/navStarsWindow.ui
)

QT5_WRAP_UI(NavStars_UIS_H ${NavStars_UIS})

SET(NavStars_RES ../resources/NavStars.qrc)
QT5_ADD_RESOURCES(NavStars_RES_CXX ${NavStars_RES})

ADD_LIBRARY(NavStars-static STATIC ${NavStars_SRCS} ${NavStars_RES_CXX} ${NavStars_UIS_H})
TARGET_LINK_LIBRARIES(NavStars-static Qt5::Core Qt5::Widgets)
SET_TARGET_PROPERTIES(NavStars-static PROPERTIES OUTPUT_NAME "NavStars")
SET_TARGET_PROPERTIES(NavStars-static PROPERTIES COMPILE_FLAGS "-DQT_STATICPLUGIN")
ADD_DEPENDENCIES(AllStaticPlugins NavStars-static)

SET_TARGET_PROPERTIES(NavStars-static PROPERTIES FOLDER "plugins/NavStars")

ADD_PRECOMPILED_HEADER(NavStars-static "NavStars.hpp" "NavStars.cpp")
