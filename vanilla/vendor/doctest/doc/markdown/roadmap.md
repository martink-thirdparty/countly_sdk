## Roadmap

This library is free, and will stay free but needs your support to sustain its development. There are lots of [**new features**](roadmap.md) and maintenance to do. If you work for a company using **doctest** or have the means to do so, please consider financial support.

[![Patreon](https://cloud.githubusercontent.com/assets/8225057/5990484/70413560-a9ab-11e4-8942-1a63607c0b00.png)](http://www.patreon.com/onqtam)
[![PayPal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.me/onqtam/10)

Planned features for future releases - order changes constantly... Also look through the [**issues**](https://github.com/onqtam/doctest/issues).

### For 2.4:

- https://github.com/onqtam/doctest/issues/208
- reporters:
    - xUnit/junit/TeamCity reporter - perhaps related: https://github.com/ujiro99/doctest-junit-report
    - compact reporter
    - options
        - absolutely no output on success (AKA quiet mode)
        - summary only (verbosity levels?)
- matchers - should investigate what they are - look at google test/mock and Catch (also predicates and boost test)
- header with extensions
    - demangling with the use of the cxxabi header
    - stringification of types from std, also enums with the help of traits as discussed in #121
    - esoteric reporters
- convolution support for the assertion macros (with a predicate)
- Value-Parameterized test cases
- generators? - look at Catch - and investigate what they are (also SUBCASEs can be while() loops instead of if() statements! that might be useful...)
- look at property based testing
    - [rapidcheck](https://github.com/emil-e/rapidcheck)
    - [autocheck](https://github.com/thejohnfreeman/autocheck)
    - [CppQuickCheck](https://github.com/grogers0/CppQuickCheck)
- proper conan package - https://github.com/onqtam/doctest/issues/103
- IDE integration
    - https://blogs.msdn.microsoft.com/vcblog/2017/05/10/unit-testing-and-the-future-announcing-the-test-adapter-for-google-test/
    - https://www.reddit.com/r/cpp/comments/65c0f1/run_cpp_unit_tests_from_xcode_and_visual_studio/
    - https://github.com/k-brac/CUTI
    - https://github.com/csoltenborn/GoogleTestAdapter
    - MSTest
        - http://accu.org/index.php/journals/1851
        - https://msdn.microsoft.com/en-us/library/hh270865.aspx
        - https://msdn.microsoft.com/en-us/library/hh598953.aspx
        - https://blogs.msdn.microsoft.com/vcblog/2017/04/19/cpp-testing-in-visual-studio/
        - https://msdn.microsoft.com/en-us/library/hh419385.aspx
    - XCode - https://github.com/catchorg/Catch2/pull/454
    - CLion
        - https://www.jetbrains.com/clion/features/unit-testing.html
        - https://blog.jetbrains.com/clion/2017/03/clion-2017-1-released/#catch

### For 2.5:

- log levels - like in [boost test](http://www.boost.org/doc/libs/1_63_0/libs/test/doc/html/boost_test/utf_reference/rt_param_reference/log_level.html)
- running tests a [few times](https://github.com/google/googletest/blob/master/googletest/docs/AdvancedGuide.md#repeating-the-tests)
- test execution in [separate processes](https://github.com/catchorg/Catch2/issues/853) - ```fork()``` for UNIX and [this](https://github.com/nemequ/munit/issues/2) for Windows
- killing a test that exceeds a time limit (will perhaps require threading or processes)
- [symbolizer](https://github.com/facebook/folly/tree/master/folly/experimental/symbolizer) - for a stack trace - when an assertion fails - and it's in a user function with some deep callstack away from the current test case - how to know the exact code path that lead to the failing assert
- ability to make the framework not capture unexpected exceptions - as requested [here](https://github.com/onqtam/doctest/issues/12#issuecomment-235334585)
- add Approx ability to compare with absolute epsilon - [Catch PR](https://github.com/catchorg/Catch2/pull/538)
- ability to customize the colors in the console output (may also use styles - based on [this](https://github.com/agauniyal/rang) or [this](https://github.com/ikalnytskyi/termcolor))
- implement breaking into the debugger under linux - see [here](https://github.com/catchorg/Catch2/pull/585) and [here](https://github.com/scottt/debugbreak)
- better testing of the library
    - unit test the String class
    - should unit test internals - currently even if a bug is caught by different output it's very difficult to track the reason
    - should test stuff that should not compile
        - https://github.com/ldionne/dyno/blob/master/cmake/CompileFailTest.cmake
        - see slide 38 here - https://github.com/boostcon/cppnow_presentations_2017/blob/master/05-19-2017_friday/effective_cmake__daniel_pfeifer__cppnow_05-19-2017.pdf
    - should test crash handling
    - should test more config options
    - don't cheat for maxing out code coverage (see [coverage_maxout.cpp](../../examples/all_features/coverage_maxout.cpp))
    - should test C++11 stuff - perhaps inspect the CMAKE_CXX_FLAGS for -std=c++11 on the CI and add more targets/tests
    - test tricky stuff like expressions with commas in asserts

### For 3.0:

- use modules - use ```std::string``` and whatever else comes from the standard - no more hand rolled traits and classes
- minimize the use of the preprocessor
- remove backwards-compatible macros for the fast asserts

### Things that are being considered but not part of the roadmap yet:

- add ability to print a diff for strings/values instead of the whole 2 versions (gtest does that)
- add LIKELY & friends for the conditions of asserts - look at BOOST_LIKELY, ppk_assert, foonathan/debug_assert, etc
- ability for users to register their own command line options and access them later on
- fix this: https://github.com/catchorg/Catch2/issues/1292
- FakeIt mocking integration - like [catch](https://github.com/eranpeer/FakeIt/tree/master/config/catch) (also checkout [this](https://github.com/ujiro99/doctest-sample))
- look into https://github.com/cpp-testing/GUnit - https://www.youtube.com/watch?v=NVrZjT5lW5o
- consider the following 2 properties for the MSVC static code analyzer: EnableCppCoreCheck, EnableExperimentalCppCoreCheck
- rpm package? like this: https://github.com/vietjtnguyen/argagg/blob/master/packaging/rpm/argagg.spec
- get the current test case/section path - https://github.com/catchorg/Catch2/issues/522
- when no assertion is encountered in a test case it should fail - and should also add a SUCCEED() call
- failure reporting should print out previous SECTIONs for data-driven testing - as requested [here](https://github.com/catchorg/Catch2/issues/734)
- ```Bitwise()``` class that has overloaded operators for comparison - to be used to check objects bitwise against each other
- detect floating point exceptions
- checkpoint/passpoint - like in [boost test](http://www.boost.org/doc/libs/1_63_0/libs/test/doc/html/boost_test/test_output/test_tools_support_for_logging/checkpoints.html) (also make all assert/subcase/logging macros to act as passpoints and print the last one on crashes or exceptions)
- queries for the current test case - name (and probably decorators)
- support for LibIdentify
- add CHECKED_IF & friends: https://github.com/catchorg/Catch2/issues/1278
- support for running tests in parallel in multiple threads
- death tests - as in [google test](https://github.com/google/googletest/blob/master/googletest/docs/AdvancedGuide.md#death-tests)
- config options
    - test case name uniqueness - reject the ones with identical names
- command line options
    - ability to specify ASC/DESC for the order option
    - global timeout option (per test or per entire session?)
    - command line error handling/reporting
    - option to not print context info when the --success option is used
    - ability for the user to extend the command line - as requested [here](https://github.com/catchorg/Catch2/issues/622)
    - option to list files in which there are test cases who match the current filters
    - option for filters to switch from "match any" to "match all" mode
    - option to list test suites and test cases in a tree view
    - add a "wait key" option (before and after tests) - as requested [here](https://github.com/catchorg/Catch2/issues/477#issuecomment-256417686)
- decorators for test cases and test suites- like in boost test
    - depends_on
    - precondition
    - fixture
    - label (tag) - with the ability to have multiple labels (tags) for a test case and also the ability to list them
    - run X times (should also multiply with (or just override) the global test run times)
    - throw an exception when incompatible decorators are given in the same list of decorators - like may_fail and should_fail
- setup / teardown support
    - global setup / teardown - can be currently achieved by providing a custom main function
    - per test suite (block? only? and not all blocks of the same test suite?)
    - as decorators
    - see how it's done in boost test - with the fixture decorator
    - perhaps for fixtures in addition to the constructor / destructor - since throwing in the destructor might terminate the program
    - or just ignore all of this this - it would require globals or classes and inheritance - and we already have subcases
- doctest in a GUI environment? with no console? APIs for attaching a console? querying if there is one? [investigate...](https://github.com/catchorg/Catch2/blob/master/docs/configuration.md#stdout)
- runtime performance
    - look at this: https://github.com/catchorg/Catch2/issues/1086
    - startup - the set holding all registered tests should use a specialized allocator to minimize program startup time
    - optimize the mutex lock:
        - http://preshing.com/20111124/always-use-a-lightweight-mutex/
        - http://preshing.com/20120226/roll-your-own-lightweight-mutex/
- ability to provide a temp folder that is cleared between each test case
- make the _MESSAGE assert macros work with variadic arguments - and maybe write the ones for binary/unary asserts as well
- move from operator "<<" to "<=" for capturing the left operand when decomposing binary expressions with templates
- think about silencing warnings about unused variables when DOCTEST_CONFIG_DISABLE is used - see commit 6b61e8aa3818c5ea100cedc1bb48a60ea10df6e8 or issue #61
    - also this: ```(void)(true ? (void)0 : ((void)(expression)))```
- think about optionally using ```<typeinfo>``` and libcxxabi for demangling so users don't have to use ```TYPE_TO_STRING()```
- handle more complex expressions - ```CHECK(foo() == 1 || bar() == 2);```
- add [[noreturn]] to MessageBuilder::react() - and actually make a separate function (react2) for the FAIL() case
- think about using a string view of some sorts
- benchmark against google test and boost test

### Things that are very unlikely to enter the roadmap:

- rethink static code analysis suppressions - users shouldn't have to use the same flags for code which uses doctest macros/types
- move the "react()" part (the one that throws for REQUIRE asserts - or for when "abort-after=<int>" is reached) to a function call in the while() part of the asserts
- stop using underscores for the begining of identifiers - the anonymous variables - against the standard...
- templated fixture test cases
- test with missed warning flags for GCC
    - https://github.com/Barro/compiler-warnings
    - http://stackoverflow.com/a/34971392/3162383
- utf8 / unicode ???
    - https://github.com/catchorg/Catch2/pull/903
- handle ```wchar``` strings???
- hierarchical test suites - using a stack for the pushed ones
- ability to specify the width of the terminal in terms of characters (for example 60 - less than 80 - the default)
- ability to re-run only newly compiled tests based on time stamps using ```__DATE__``` and ```__TIME__``` - stored in some file
- add underscores to all preprocessor identifiers not intended for use by the user
- put everything from the ```detail``` namespace also in a nested anonymous namespace to make them with internal linkage
- ability to put everything from doctest into an anonymous namespace - to allow the use of multiple different versions of **doctest** within the same binary (executable/dll) - like the [**stb**](https://github.com/nothings/stb) libraries can

---------------

[Home](readme.md#reference)

<p align="center"><img src="../../scripts/data/logo/icon_2.svg"></p>
