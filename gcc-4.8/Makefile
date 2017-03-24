#! Makefile
################################################################################
#                                                                              #
#                      Matlab Mat data convert to C++ data                   #
#                                                                              #
################################################################################
BUILD_DIR =build
PROJECT = MatlabIO

CC = g++

#
# Arguments to force ANSI specs. I only use this to make sure the code complies
# with ANSI C specs.
# 
ifeq ($(ansi),true)
	ANSI_ARGS = -ansi -pedantic -Wall -Werror
else
	ANSI_ARGS = -std=c++11 -pedantic -Wall -Werror
endif


#
# Compile arguments
#
# Runs for each file in src/. $@ is the output (.o), $< is the input (.c)
#
COMPILE = $(CC) -c -I $(INCLUDE) $(ANSI_ARGS)  -ffast-math -funroll-loops  $<

#
# Shared library arguments
#
# SHARED_LIB = $(CC) -shared -o $(LIB).so $^ -lm

SOURCES = $(wildcard src/*.cpp)
OBJECTS = $(patsubst src/%.cpp, $(BUILD_DIR)/%.o, $(SOURCES))
INCLUDE = ./include

# $(info $(OBJECTS))
# $(info $(SOURCES))
all:$(BUILD_DIR) main

$(BUILD_DIR):
	@echo "Create build directory $@"
	mkdir -p $(BUILD_DIR)

main: main.o $(OBJECTS)
	@echo "compile the target"
	$(CC) $^ -o main 

main.o: main.cpp
	$(CC) -c $< -I $(INCLUDE) $(ANSI_ARGS) -ffast-math -funroll-loops -o $@
	
$(BUILD_DIR)/%.o: src/*.cpp
	$(CC) -c $< -I $(INCLUDE) $(ANSI_ARGS) -ffast-math -funroll-loops -o $@

runtest:
	./main

clean:
	rm -f  main main.o
	rm -rf $(BUILD_DIR)