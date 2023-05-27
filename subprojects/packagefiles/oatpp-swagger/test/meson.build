test_src_files = files(
    'oatpp-swagger/AsyncControllerTest.cpp',
    'oatpp-swagger/AsyncControllerTest.hpp',
    'oatpp-swagger/ControllerTest.cpp',
    'oatpp-swagger/ControllerTest.hpp',
    'oatpp-swagger/test-controllers/TestAsyncController.hpp',
    'oatpp-swagger/test-controllers/TestController.hpp',
    'oatpp-swagger/tests.cpp',
)

test_deps = deps
test_deps += dependency('oatpp-test', version: '1.3.0')

swagger_tests = executable(
    'oatpp_swagger_tests',
    test_src_files,
    cpp_args: flags,
    include_directories: include_directories('.'),
    dependencies: test_deps,
)

test('oatpp swagger module tests', swagger_tests)
