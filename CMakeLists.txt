cmake_minimum_required(VERSION 3.16)

project(NNPrabhupadaDB LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set( CopperSpiceSrc_DIR ../../CopperSpice/Source/src )
set( PostgreSQL_ROOT:PATH=C:/Prg/PostgreSQL/17 )
set( CopperSpice_DIR:PATH=D:/CopperSpice/${CMAKE_BUILD_TYPE}/Lib/cmake/CopperSpice )
set( libpqxx_DIR:PATH=D:/CopperSpice/${CMAKE_BUILD_TYPE}Libpqxx/Lib/lib/cmake/libpqxx )
set( NNPrabhupada_LIBRARIES:PATH=${CopperSpiceSrc_DIR}/Prabhupada/build/Desktop-${CMAKE_BUILD_TYPE} )

find_package( QT NAMES Qt6 Qt5 REQUIMPONENTS Core Gui Widgets Sql )
find_package( Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Gui Widgets Sql )
find_package( libpqxx REQUIRED )
#find_package( NNPrabhupada REQUIRED )

# удалите комментарий для CopperSpice
#add_definitions( -DCS_MODE )

add_library(NNPrabhupadaDB SHARED
  NNPrabhupadaDB_global.h
  NNPrabhupadaDB.cpp
  NNPrabhupadaDB.h
  ${CopperSpiceSrc_DIR}/PrabhupadaDB/QPrabhupadaDB.cpp
  ${CopperSpiceSrc_DIR}/PrabhupadaDB/QPrabhupadaDB.h
  ${CopperSpiceSrc_DIR}/PrabhupadaDB/QPrabhupadaDBFocus.h
  ${CopperSpiceSrc_DIR}/PrabhupadaDB/QtPrabhupadaDB.h
)

target_include_directories( NNPrabhupadaDB PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/${CopperSpiceSrc_DIR}/Prabhupada)
target_include_directories( NNPrabhupadaDB PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/${CopperSpiceSrc_DIR}/PrabhupadaDB)

target_link_libraries(NNPrabhupadaDB PRIVATE
  Qt${QT_VERSION_MAJOR}::Core
  Qt${QT_VERSION_MAJOR}::Widgets
  Qt${QT_VERSION_MAJOR}::Gui
  Qt${QT_VERSION_MAJOR}::Sql
  libpqxx::pqxx
  NNPrabhupada
)

target_compile_definitions(NNPrabhupadaDB PRIVATE NNPRABHUPADADB_LIBRARY)
#target_compile_definitions(NNPrabhupadaDB PRIVATE CS_MODE)
