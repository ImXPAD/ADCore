TOP=../..
include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

# Persuade travis (ubuntu 12.04) to use HDF5 API V2 (1.8 rather than default 1.6)
USR_CXXFLAGS_Linux += -DH5_NO_DEPRECATED_SYMBOLS -DH5Dopen_vers=2

# The plugin-test executable with the actual unittests depend on the boost 
# unittest framework so we can only build it if boost has been configured
ifdef BOOST
  # The ADTestUtility library contain a number of helper functions to generate test
  # data, asyn port names, record output NDArrays etc etc.
  # This utility library can be used by external modules that provides unittests.
  LIBRARY_IOC_Linux += ADTestUtility
  ADTestUtility_SRCS += testingutilities.cpp
  ADTestUtility_SRCS += AsynPortClientContainer.cpp
  ADTestUtility_SRCS += AsynException.cpp
  ADTestUtility_SRCS += SimulatedDetectorWrapper.cpp
  ADTestUtility_SRCS += HDF5PluginWrapper.cpp
  ADTestUtility_SRCS += HDF5FileReader.cpp

  PROD_IOC_Linux += plugin-test
  plugin-test_SRCS += plugin-test.cpp
  plugin-test_SRCS += test_NDPluginCircularBuff.cpp
  plugin-test_SRCS += test_NDFileHDF5.cpp
  # Add tests for new plugins like this:
  #plugin-test_SRCS += test_<plugin name>.cpp
  
  plugin-test_LIBS += boost_unit_test_framework simDetector ADTestUtility
  boost_unit_test_framework_DIR=$(BOOST_LIB)
endif

USR_INCLUDES += $(HDF5_INCLUDE)
USR_INCLUDES += $(SZ_INCLUDE)
USR_INCLUDES += $(XML2_INCLUDE)

PROD_LIBS += NDPlugin ADBase asyn

include $(TOP)/configure/RULES
