.DEFAULT_GOAL=help
.PHONY=all

#-----------------------------------------------#
#                                               #
#      Target and libs compilation options      #
#                                               #
#-----------------------------------------------#

# Main file's name (and thus output file name)
TARGET?=main

# Libraries needed (will be compiled)
LIBS?=libname.o otherlib.o

#-----------------------------------------------#
#                                               #
#   Compilation options (edit only if needed)   #
#                                               #
#-----------------------------------------------#

# Compiler executable
CC=g++

# Compilation flags
CFLAGS?=-lm -Wall

#-----------------------------------------------#
#                                               #
#                    Recipes                    #
#                                               #
#-----------------------------------------------#

help: ## Show this help.
	@printf "\033[32m%-30s     \033[32m %s\n" "VARIABLE NAME" "DEFAULT_VALUE"
	@grep -E '^[a-zA-Z_-]+(\?=|=).*$$' $(MAKEFILE_LIST) |sort | awk 'BEGIN {FS = "(?=|=)"}; {printf "\033[36m%-30s     \033[0m %s\n", $$1, $$2}'
	@printf "\n\033[32m%-30s     \033[32m %s\033[0m\n" "RECIPE" "DESCRIPTION"
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "make \033[36m%-30s\033[0m %s\n", $$1, $$2}'

$(TARGET): $(TARGET.cpp) ## Auto build target
	$(MAKE) build

$(LIBS): %.o: %.cpp %.h ## Auto build libs
	$(CC) -c $< -o $@

build: $(TARGET).cpp $(LIBS) # Build target
	$(CC) $(TARGET).cpp -o $(TARGET) $(LIBS) $(CFLAGS)

run: $(TARGET) ## Run target (build if needed)
	./$(TARGET)

run-clean: clean run ## Cleaning before runnig (force build)

clean: ## Clean directory from compiled files
	find ./ -type f ! -name "*.*" ! -path "./Makefile" -delete
	find ./ -type f -name "*out*" -delete
	find ./ -type f -name "*.o" -delete
	find ./ -type f -name ".fuse*" -delete
