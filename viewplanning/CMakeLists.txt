cmake_minimum_required(VERSION 2.6)

project(viewplanning)

########### First configure the following ###########
set(RELATED_DIRS_DIRECTORY ${VPL_SOURCE_DIR}/..)

#set(SRC_ROBOTS vprobot.cpp robotmobile.cpp robotarmmdh.cpp vprfreeflyer.cpp robotcomposed.cpp)
set(SRC_ROBOTS vprobot.cpp vprfreeflyer.cpp)
#set(REALROBOT_SRC robotpioneer.cpp robotkatana.cpp)

set(SRC_SENSORS rangesensor.cpp)
#set(SRC_SENSORS rangesensor.cpp rskinect.cpp rssimulated.cpp rsblensor.cpp)
#set(SRC_OCTREE_RSIM rssraytracingoctree.cpp)

set(SRC_ROBOTSENSOR robotsensor.cpp robsennotransformation.cpp)

#set(SRC_NBVPLANNER nbvplannerrgflt.cpp nbvplanner.cpp  workspacenbvplanner.cpp  rrtnbv.cpp nbvplannerexpectedutility.cpp nbvplannerexpectedutilitynroot.cpp)
set(SRC_NBVPLANNER nbvplanner.cpp  workspacenbvplanner.cpp)

#set(SRC_RECONSTRUCTOR reconstructor3d.cpp r3ddirectpositioning.cpp vplutils.cpp)
set(SRC_RECONSTRUCTOR reconstructor3d.cpp r3ddirectpositioning.cpp vplutils.cpp)

set(SRC_ALL ${SRC_ROBOTS} ${SRC_SENSORS} ${SRC_NBVPLANNER} ${SRC_ROBOTSENSOR} ${SRC_RECONSTRUCTOR})


#---------------- Partial Model Library ---------
include_directories(${VPL_SOURCE_DIR}/partialmodel)
link_directories(${VPL_SOURCE_DIR}/lib)
set(LIBS_PARTIAL_MODEL PartialModel)


# --------------- Octomap --------------------
find_package(octomap REQUIRED)
include_directories(${OCTOMAP_INCLUDE_DIRS})
set(LIBS_OCTOMAP ${OCTOMAP_LIBRARIES})


# ---------------- MRPT ---------------------
 find_package(MRPT REQUIRED)
 include_directories(${MRPT_INCLUDE_DIRS})
 link_directories(${MRPT_LINK_DIRECTORIES})
# include_directories(/usr/include/mrpt/gui/include)
 set(LIBS_MRPT mrpt-base)


set (ALL_LIBS ${LIBS_PARTIAL_MODEL} ${LIBS_OCTOMAP} ${LIBS_MRPT})

# -------------------------------------------------
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${VPL_SOURCE_DIR}/lib)
add_library(ViewPlanning SHARED ${SRC_ALL})