project(
    'crud',
    'cpp',
    default_options: [
        'buildtype=release',
        'optimization=3',
        'strip=true',
        'cpp_std=c++11',
        'b_ndebug=if-release',
        'default_library=static',
    ],
)


deps = []
deps += dependency('oatpp', version: '1.3.0', default_options: ['tests=false'])
deps += dependency('oatpp-swagger', version: '1.3.0')
deps += dependency('oatpp-sqlite', version: '1.3.0')

deps += dependency('threads')


flags = [
    '-DDATABASE_FILE="' + (meson.project_source_root() / 'db.sqlite') + '"',
    '-DDATABASE_MIGRATIONS="' + (meson.project_source_root() / 'sql') + '"',
]


crud_lib = library(
    'crud',
    files(
        'src/AppComponent.hpp',
        'src/DatabaseComponent.hpp',
        'src/ErrorHandler.cpp',
        'src/ErrorHandler.hpp',
        'src/SwaggerComponent.hpp',
        'src/controller/StaticController.hpp',
        'src/controller/UserController.hpp',
        'src/db/UserDb.hpp',
        'src/dto/PageDto.hpp',
        'src/dto/StatusDto.hpp',
        'src/dto/UserDto.hpp',
        'src/service/UserService.cpp',
        'src/service/UserService.hpp',
    ),
    include_directories: include_directories('src'),
    dependencies: deps,
    cpp_args: flags,
    override_options: ['warning_level=3', 'werror=false'],
)


executable(
    'crud',
    files('src/App.cpp'),
    include_directories: include_directories('src'),
    dependencies: deps,
    cpp_args: flags,
    link_with: crud_lib,
    override_options: ['warning_level=3', 'werror=false'],
)


if get_option('tests')

    test_deps = deps
    test_deps += dependency('oatpp-test', version: '1.3.0')

    crud_test = executable(
        'crud_test',
        files(
            'test/UserControllerTest.cpp',
            'test/UserControllerTest.hpp',
            'test/app/TestClient.hpp',
            'test/app/TestComponent.hpp',
            'test/app/TestDatabaseComponent.hpp',
            'test/tests.cpp',
        ),
        include_directories: include_directories('test', 'src'),
        link_with: crud_lib,
        dependencies: test_deps,
        override_options: ['warning_level=1', 'werror=false'],
    )
    test('Crud Tests', crud_test)

endif

