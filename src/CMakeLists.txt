include (FindPkgConfig)
pkg_search_module (urg REQUIRED urg0.8)
pkg_search_module (playercore REQUIRED playercore)

if (NOT PKG_CONFIG_FOUND)
	message(FATAL_ERROR "Cannot find pkg-config!")
endif ()

include_directories (${urg_INCLUDE_DIRS} ${playercore_INCLUDE_DIRS})
add_library (playerurg2 SHARED playerurg.cpp)
target_link_libraries (playerurg2 ${urg_LIBRARIES} ${playercore_LIBRARIES})

set_target_properties (playerurg2 PROPERTIES
  VERSION 0.0.1
  SOVERSION 0.0.1)

install(TARGETS playerurg2 DESTINATION lib COMPONENT libraries)
install(FILES urglaser.cfg DESTINATION  share/player/config)
