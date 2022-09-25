cmake_minimum_required(VERSION 3.18)
file(STRINGS "${CMAKE_CURRENT_SOURCE_DIR}/version.txt" VERSION)
project(simpson VERSION "${VERSION}" LANGUAGES C)

set(
        CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH}" "${PROJECT_SOURCE_DIR}/cmake"
        CACHE STRING "" FORCE
)

find_package(MPI)
find_package(CBLAS)
find_package(LAPACK)
find_package(LAPACKE)
find_package(TCL)
find_package(FFTW3)
find_package(NFFT)

add_library(libsimpson 
allocation.c
auxmath.c
averaging.c
B0inhom.c
blockdiag.c
cm.c
complx.c
cryst.c
crystdat.c
distortions.c
fft.c
fidcalc.c
ftools.c
ham.c
iodata.c
isotopes.c
lbfgs.c
matrix.c
OCroutines.c
pthread_barrier_mac.c
pulse.c
readsys.c
relax.c
rfprof.c
rfshapes.c
sim.c
simpson.c
spinach.c
spinsys.c
tclcode.c
tclutil.c
wigner.c)

add_executable(simpson 
main.c)

target_link_libraries(simpson LINK_PUBLIC libsimpson ${NFFT_LIBRARIES} ${FFTW3_LIBRARY} ${TCL_LIBRARY} ${LAPACKE_LIBRARIES} ${LAPACK_LIBRARIES} ${CBLAS_LIBRARIES} ${MPI_mpi_LIBRARY} m)

