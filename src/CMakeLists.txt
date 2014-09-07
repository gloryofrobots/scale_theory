find_package(Sphinx REQUIRED)

SET(DOC_FILES
    src/index.rst
    src/scales.rst
)

SET(DOC_DIRS
    _static
    _templates
)

if(NOT DEFINED SPHINX_THEME)
    set(SPHINX_THEME agogo)
endif()

if(NOT DEFINED SPHINX_THEME_DIR)
    set(SPHINX_THEME_DIR)
endif()

# configured documentation tools and intermediate build results
set(BINARY_BUILD_DIR "${DOCS_TEMP_DIR}/_build")

# Sphinx cache with pickled ReST documents
set(SPHINX_CACHE_DIR "${DOCS_TEMP_DIR}/_doctrees")

# HTML output directory
set(SPHINX_HTML_DIR "${DOCS_OUTPUT_DIR}/html")

configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/conf.py.in"
    "${BINARY_BUILD_DIR}/conf.py"
    @ONLY)

foreach(_dir ${DOC_DIRS})
    execute_process(COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/${_dir}
                                                           ${BINARY_BUILD_DIR}/${_dir})

endforeach()

add_custom_target(docs-html ALL
    ${SPHINX_EXECUTABLE}
        -q -b html
        -c "${BINARY_BUILD_DIR}"
        -d "${SPHINX_CACHE_DIR}"
        "${CMAKE_CURRENT_SOURCE_DIR}"
        "${SPHINX_HTML_DIR}"
    COMMENT "Building HTML documentation with Sphinx")

