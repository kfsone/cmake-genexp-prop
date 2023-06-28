cmake_minimum_required (VERSION 3.17)
project (test LANGUAGES C)

add_library (l1 STATIC f1.c)
set_property (TARGET l1 PROPERTY FOO "FOO property from l1")
target_compile_definitions (l1 PUBLIC -DBAR="public Dbar from l1")
target_compile_definitions (l1 PRIVATE -DBAR="Dbar from l1")

add_library (l2 STATIC f2.c)
target_link_libraries (l2 PUBLIC l1)
target_compile_definitions (l2 PRIVATE -DFOO_L1="$<TARGET_PROPERTY:l1,FOO>")
target_compile_definitions (l2 PRIVATE -DFOO_L2="$<TARGET_PROPERTY:l2,FOO>")

add_executable (test main.c)
target_link_libraries (test l2)
