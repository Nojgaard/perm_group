if(NOT BUILD_DOC)
    return()
endif()

set(output ${CMAKE_CURRENT_BINARY_DIR}/html)
set(doctrees ${CMAKE_CURRENT_BINARY_DIR}/doctrees)
add_custom_target(perm_group_doc
        COMMAND ${SPHINX} ${CMAKE_CURRENT_SOURCE_DIR}/source -b html ${output} -d ${doctrees})
if(TARGET doc)
    add_dependencies(doc perm_group_doc)
else()
    add_custom_target(doc ALL DEPENDS perm_group_doc)
endif()
set_directory_properties(PROPERTIES ADDITIONAL_MAKE_CLEAN_FILES ${output})
install(DIRECTORY ${output}
        DESTINATION ${CMAKE_INSTALL_DOCDIR}
        COMPONENT PermGroup_doc)