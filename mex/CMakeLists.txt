if (NOT BUILD_MEX)
    unset(MATLAB_MCC CACHE)
    unset(MATLAB_MEX CACHE)
    unset(MATLAB_MEXEXT CACHE)
    unset(MATLAB_ROOT CACHE)
    unset(BUILD_MEX_TESTS CACHE)
    return()
endif()

include(${CMAKE_SOURCE_DIR}/cmake/matlab.cmake REQUIRED)

option(BUILD_MEX_TESTS "Build matlab mex tests" ON)

configure_file(Segy.m Segy.m)
configure_file(SegySpec.m SegySpec.m)
configure_file(SegySampleFormat.m SegySampleFormat.m)
configure_file(TraceSortingFormat.m TraceSortingFormat.m)
configure_file(TraceField.m TraceField.m)


mexo(segyutil)
mex(segyspec_mex)
mex(segy_read_write_line_mex segyutil)
mex(segy_read_write_ps_line_mex segyutil)
mex(segy_get_header_mex segyutil)
mex(segy_get_traces_mex segyutil)
mex(segy_put_traces_mex segyutil)
mex(segy_get_ntraces_mex segyutil)
mex(segy_get_segy_header_mex segyutil)
mex(segy_get_bfield_mex segyutil)
mex(segy_get_trace_header_mex segyutil)
mex(segy_get_field_mex segyutil)
mex(segy_put_headers_mex segyutil)
mex(segy_get_offsets_mex segyutil)

install(FILES
        ${CMAKE_CURRENT_BINARY_DIR}/segyspec_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_read_write_line_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_read_write_ps_line_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_header_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_traces_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_put_traces_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_ntraces_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_segy_header_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_bfield_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_trace_header_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_field_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_put_headers_mex.mexa64
        ${CMAKE_CURRENT_BINARY_DIR}/segy_get_offsets_mex.mexa64
        SegySpec.m
        Segy.m
        SegySampleFormat.m
        TraceSortingFormat.m
        TraceField.m
        DESTINATION
        ${CMAKE_INSTALL_PREFIX}/matlab)
