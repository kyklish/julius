
include_directories(.)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} --coverage")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} --coverage")

set(TESTS
    core/buffer
    core/calc
    core/dir
    core/file
    core/io
    core/random
    core/string
    core/time
    core/zip

    building/model
    
    empire/trade_prices
    
    figure/name
    
    game/time
)

foreach (testcase ${TESTS})
    string(REPLACE "/" "_" testname ${testcase})
    add_executable(${testname}_test ../src/${testcase}.c ${testcase}_test.c)
    add_test(NAME ${testname} COMMAND ${testname}_test)
endforeach (testcase)

file(COPY data DESTINATION ${CMAKE_CURRENT_BINARY_DIR})