ADD_LIBRARY(miner SHARED
	Miner
	MinerUtils
	HandleTree
	Valuations
   Surprisingness
)

TARGET_LINK_LIBRARIES(miner
	${COGUTIL_LIBRARY}
	${ATOMSPACE_LIBRARIES}
)

INSTALL (TARGETS miner DESTINATION "lib${LIB_DIR_SUFFIX}/opencog")

INSTALL (FILES
	Miner.h
	MinerUtils.h
	HandleTree.h
	Valuations.h
	Surprisingness.h
	DESTINATION "include/opencog/learning/miner"
)

IF (HAVE_GUILE)
  ADD_LIBRARY(guile-miner SHARED
    MinerSCM
  )

  TARGET_LINK_LIBRARIES(guile-miner
    miner
    ${GUILE_LIBRARIES}
  )

  INSTALL (TARGETS guile-miner DESTINATION "lib${LIB_DIR_SUFFIX}/opencog")

  ADD_GUILE_MODULE (FILES
    miner.scm
    miner-utils.scm
    MODULE_DESTINATION "${GUILE_SITE_DIR}/opencog/miner"
  )

  ADD_SUBDIRECTORY (rules)
ENDIF (HAVE_GUILE)
