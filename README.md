CMake experiment with generator expressions and property inheritance
--------------------------------------------------------------------

*Theory*: a property on a library is visible thru inheritance at
compile time.

This example links `l1` as a dependency on `l2` and then attempts to
surface `$<TARGET_PROPERTY:l1,FOO>` and `$<TARGET_PROPERTY:l2,FOO>` to
test whether the value is inherited upwards.

*Conclusion*: The `l2,FOO` is empty, indicating that - for `target_compile_definitions`
at least - you cannot see an inherited property.

*Note*: This does not eliminate the possibility the property could be seen
at link time or in other expressions.
