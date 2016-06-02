project (recurse C)

add_executable(recurse1 ex-1.c)
target_link_libraries(recurse1 cadt)

add_executable(recurse2 ex-2.c)
target_link_libraries(recurse2 cadt)
