include ../../environment_variables.mk 

PROJECT_NAME := server
CPP_FILES := $(wildcard *.cpp)
CPP_FILES += $(wildcard ../metadata/*.cc)
CPP_FILES += $(wildcard ../protocol/*.cpp)
OBJ_FILES := $(addprefix ${BUILDDIR}/,$(notdir $(CPP_FILES:.cpp=.o)))
OBJ_FILES := $(OBJ_FILES:.cc=.o)

all: $(BUILDDIR) $(BUILDDIR)/${PROJECT_NAME}

clean:
	rm -r ${BUILDDIR}/${PROJECT_NAME} ${OBJ_FILES}

$(BUILDDIR)/${PROJECT_NAME}: ${OBJ_FILES} 
	${CPP_COMPILER} -g -lpthread -lboost_system -lprotobuf -ldl -o $@ $^ 
	
${BUILDDIR}/%.o: %.cpp 
	${CPP_COMPILER}  -g -DAPPS_LIBRARY_PATH=\"$(abspath $(BUILDDIR)/libsimple.so)\" -std=c++11 ${COMPILER_FLAGS} -c $< -o $@  

${BUILDDIR}/%.o: ../metadata/%.cc 
	${CPP_COMPILER} -std=c++11 -g ${COMPILER_FLAGS} -c $< -o $@  

${BUILDDIR}/%.o: ../protocol/%.cpp 
	${CPP_COMPILER} -std=c++11 -g ${COMPILER_FLAGS} -c $< -o $@  

${BUILDDIR}:
	mkdir -p ${BUILDDIR}
