include("../cmake/Findlibmemcached.cmake")
include("../cmake/Findthrift.cmake")
include("../cmake/FindLibevent.cmake")

include_directories("/home/kang222/projects/rpu-scalar/thrift-install/include")
include_directories("/home/kang222/projects/rpu-scalar/libmemcached-1.0.9/build/include")
include_directories("/home/kang222/projects/rpu-scalar/yaml-cpp-install/include")
include_directories("/home/kang222/projects/rpu-scalar/jwt-install/include")
include_directories("/home/kang222/projects/rpu-scalar/opentracing-install/include")
include_directories("/home/kang222/projects/rpu-scalar/jaeger-install/include")
include_directories("/home/kang222/projects/rpu-scalar/redis-install/include")
include_directories("/home/kang222/projects/rpu-scalar/hiredis-install/include")

link_directories($HOME/projects/rpu-scalar/jaeger-install/lib)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(libmongoc-1.0 1.13 REQUIRED)
find_package(nlohmann_json 3.5.0 REQUIRED)
find_package(Threads)
find_package(OpenSSL REQUIRED)
find_package(amqpcpp REQUIRED)

set(Boost_USE_STATIC_LIBS ON)
#set(Boost_DEBUG ON)
set(Boost_NO_BOOST_CMAKE ON)
find_package(Boost 1.54.0 REQUIRED COMPONENTS log log_setup program_options)
if(Boost_FOUND)
  include_directories(${Boost_INCLUDE_DIRS})
  link_directories(${Boost_LIBRARY_DIRS})
endif()

#set(POCO_PREFIX      "/usr/local")
#set(POCO_INCLUDE_DIR "${POCO_PREFIX}/include")
#set(POCO_LIB_DIR     "${POCO_PREFIX}/lib")
#set(POCO_LIBS        "${POCO_LIB_DIR}/libPocoNet.so"
#                     "${POCO_LIB_DIR}/libPocoUtil.so"
#                     "${POCO_LIB_DIR}/libPocoFoundation.so")


add_library(jaegertracing SHARED IMPORTED)
set_target_properties(jaegertracing PROPERTIES IMPORTED_LOCATION
    /home/kang222/projects/rpu-scalar/jaeger-install/lib/libjaegertracing.so)

#add_library(redis++ SHARED IMPORTED)
#set_target_properties(redis++ PROPERTIES IMPORTED_LOCATION
#    /home/kang222/projects/rpu-scalar/redis-install/lib/libredis++.so)

#add_library(cpp_redis STATIC IMPORTED)
#set_target_properties(cpp_redis PROPERTIES IMPORTED_LOCATION
#    /usr/local/lib/libcpp_redis.a)
#
#add_library(tacopie STATIC IMPORTED)
#set_target_properties(tacopie PROPERTIES IMPORTED_LOCATION
#    /usr/local/lib/libtacopie.a)



set(THRIFT_GEN_CPP_DIR ../../gen-cpp)

add_subdirectory(TextService)
add_subdirectory(UniqueIdService)
add_subdirectory(UserService)
add_subdirectory(SocialGraphService)
# add_subdirectory(WriteHomeTimelineService)
add_subdirectory(PostStorageService)
add_subdirectory(UserTimelineService)
add_subdirectory(ComposePostService)
add_subdirectory(UserMentionService)
add_subdirectory(UrlShortenService)
add_subdirectory(MediaService)
add_subdirectory(HomeTimelineService)
