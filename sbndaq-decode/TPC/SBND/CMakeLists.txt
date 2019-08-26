simple_plugin( SBNDTPCDecoder module
  sbndaqMode
  sbnddaq-datatypes_Overlays 
  sbnddaq-datatypes_NevisTPC
  ${LARDATAOBJ}
  lardataobj_RawData
  ${ART_UTILITIES}
  ${FHICLCPP}
  ${MF_MESSAGELOGGER}
  ${MF_UTILITIES}
  ${ART_FRAMEWORK_CORE}
  ${ROOT_BASIC_LIB_LIST}
)

install_headers()
install_fhicl()
install_source()

