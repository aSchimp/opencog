INCLUDE_DIRECTORIES (
	${PROJECT_SOURCE_DIR}/opencog/atomspace
	${PROJECT_SOURCE_DIR}/opencog/query
	${PROJECT_SOURCE_DIR}/opencog/util
)

LINK_DIRECTORIES(
	${PROJECT_BINARY_DIR}/opencog/nlp/types
	${PROJECT_BINARY_DIR}/opencog/atomspace
	${PROJECT_BINARY_DIR}/opencog/query
	${PROJECT_BINARY_DIR}/opencog/util
)

LINK_LIBRARIES(
	atomspace
	nlp-types
	query
	server
	${Boost_SIGNALS_LIBRARY}
)

# We want to run the tests in the order below;
# Each test gets progressively more complex, and exercises
# features that the later tests depend on.
ADD_CXXTEST(PatternUTest)
ADD_CXXTEST(StackUTest)
ADD_CXXTEST(BigPatternUTest)
ADD_CXXTEST(BiggerPatternUTest)
ADD_CXXTEST(LoopPatternUTest)
ADD_CXXTEST(BooleanUTest)
ADD_CXXTEST(Boolean2NotUTest)

# Its a *lot* easier to write scheme, than to write C++ code!
IF (HAVE_GUILE)
	ADD_CXXTEST(ImplicationUTest)
	ADD_CXXTEST(ExecutionUTest)
	ADD_CXXTEST(BuggyStackUTest)
	ADD_CXXTEST(VarTypeNotUTest)
	ADD_CXXTEST(MatchLinkUTest)
	ADD_CXXTEST(UnorderedUTest)
	ADD_CXXTEST(StackMoreUTest)

	TARGET_LINK_LIBRARIES(VarTypeNotUTest
		cogutil
	)
ENDIF (HAVE_GUILE)

