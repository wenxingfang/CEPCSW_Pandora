
gaudi_subdir(Examples v0r0)

find_package(podio REQUIRED)
#find_package(plcio REQUIRED)
find_package(LCIO REQUIRED)
find_package(EDM4HEP REQUIRED)
find_package(K4FWCore REQUIRED)

set(Examples_srcs
    src/Edm4hepTest/*.cpp
)

# Headers and Libraries

gaudi_install_headers(Examples)

# Modules
gaudi_add_module(Examples ${Examples_srcs}
    INCLUDE_DIRS K4FWCore GaudiAlgLib GaudiKernel ${podio_INCLUDE_DIRS} ${LCIO_INCLUDE_DIRS}
    LINK_LIBRARIES K4FWCore GaudiAlgLib GaudiKernel ${LCIO_LIBRARIES} 
      # Force loading the libraries.
      -Wl,--no-as-needed EDM4HEP::edm4hep EDM4HEP::edm4hepDict ${podio_LIBRARIES} podio::podioRootIO -Wl,--as-needed
)

# Unit tests




gaudi_add_test(Edm4hepWriteAlg
               FRAMEWORK options/edm4hep_write.py)

gaudi_add_test(Edm4hepReadAlg
               FRAMEWORK options/edm4hep_read.py)

