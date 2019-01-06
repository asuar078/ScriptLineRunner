include(ExternalProject)


###############################################################################
# HumbleLogging
###############################################################################

ExternalProject_Add(
  HumbleLogging

  GIT_REPOSITORY "https://github.com/mfreiholz/humble-logging-library.git"
  GIT_TAG "master"

  UPDATE_COMMAND ""
  PATCH_COMMAND ""

  SOURCE_DIR "${CMAKE_SOURCE_DIR}/3rdparty/humblelogging"
  CMAKE_ARGS -DBuildShared=ON -DBuildExamples=OFF -DCMAKE_INSTALL_PREFIX=${GLOBAL_OUTPUT_PATH}/humblelogging

  TEST_COMMAND ""
)

ExternalProject_Add_Step(
  HumbleLogging CopyToBin
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${GLOBAL_OUTPUT_PATH}/humblelogging/bin ${GLOBAL_OUTPUT_PATH}
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${GLOBAL_OUTPUT_PATH}/humblelogging/lib ${GLOBAL_OUTPUT_PATH}
  DEPENDEES install
)

set(HumbleLogging_INCLUDE_DIRS "${CMAKE_SOURCE_DIR}/3rdparty/humblelogging/include")
set(HumbleLogging_LIBRARIES "${CMAKE_SHARED_LIBRARY_PREFIX}humblelogging${CMAKE_SHARED_LIBRARY_SUFFIX}")
include_directories(${HumbleLogging_INCLUDE_DIRS})

# https://gitlab.freedesktop.org/poppler/poppler.git

###############################################################################
# Poppler
###############################################################################

ExternalProject_Add(
  Poppler

  GIT_REPOSITORY "https://gitlab.freedesktop.org/poppler/poppler.git"
  GIT_TAG "master"

  UPDATE_COMMAND ""
  PATCH_COMMAND ""

  SOURCE_DIR "${CMAKE_SOURCE_DIR}/3rdparty/poppler"
  CMAKE_ARGS -DBuildShared=ON -DBuildExamples=OFF -DCMAKE_INSTALL_PREFIX=${GLOBAL_OUTPUT_PATH}/poppler

  TEST_COMMAND ""
)

ExternalProject_Add_Step(
  Poppler CopyToBin
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${GLOBAL_OUTPUT_PATH}/poppler/lib ${GLOBAL_OUTPUT_PATH}
  DEPENDEES install
)

set(Poppler_QT5_INCLUDE_DIRS "${CMAKE_SOURCE_DIR}/3rdparty/poppler/qt5/src")
set(Poppler_QT5_LIBRARIES "${CMAKE_SHARED_LIBRARY_PREFIX}poppler-qt5${CMAKE_SHARED_LIBRARY_SUFFIX}")
include_directories(${Poppler_QT5_INCLUDE_DIRS})

message(status "pop include: ${Poppler_QT5_INCLUDE_DIRS}")
