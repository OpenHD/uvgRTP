project(uvgrtp_test)

enable_testing()
include(GoogleTest)

add_executable(${PROJECT_NAME})
target_sources(${PROJECT_NAME}
        PRIVATE
            main.cpp
            test_1_version.cpp
            test_2_rtp.cpp
            test_3_rtcp.cpp
            test_4_formats.cpp
            test_5_srtp_zrtp.cpp
            test_6_scl_unit_test.cpp
            test_common.hh
        )

target_include_directories(${PROJECT_NAME}
        PRIVATE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../src>
        )
        
target_link_libraries(${PROJECT_NAME}
    PRIVATE
        GTest::GTestMain
        uvgrtp
    )

if(CRYPTOPP_FOUND)
    if(MSVC)
        target_link_libraries(${PROJECT_NAME}
            PRIVATE
                cryptlib
            )
    else()
        target_link_libraries(${PROJECT_NAME}
            PRIVATE
                cryptopp
            )
    endif()
endif()

gtest_add_tests(
        TARGET ${PROJECT_NAME}
)