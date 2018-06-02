BUILD = build
SOURCE_DIR = src
SOURCEGLAD_DIR= GLAD
BINARY = $(BUILD)/executable
COMPILER = g++
LIBS = -lm -lGL -lGLU -lglfw3 -lX11 -lXxf86vm -lXrandr -lpthread -lXi -ldl -lXinerama -lXcursor -lglut
####DEFINIZIONE PATH CARTELLE###
SRCSG = $(shell find $(SOURCEGLAD_DIR) -name '*.c')
SRCS = $(shell find $(SOURCE_DIR) -name '*.cpp')
###########
#######RACCOLTA FILE C E CPP###########
OBJS = $(patsubst $(SOURCE_DIR)%.cpp,$(BUILD)%.o, $(SRCS)) $(patsubst $(SOURCEGLAD_DIR)%.c,$(BUILD)%.o, $(SRCSG))
DEPS = $(patsubst $(SOURCE_DIR)%.cpp,$(BUILD)%.d, $(SRCS)) $(patsubst $(SOURCEGLAD_DIR)%.c,$(BUILD)%.d, $(SRCSG))
##############################
###COMPILAZIONE############
all: $(BINARY)
#####GLAD#####
$(BUILD)/%.o: $(SOURCEGLAD_DIR)/%.c
	$(COMPILER) $(LIBS) -c $< -o $@
$(BUILD)/%.d: $(SOURCEGLAD_DIR)/%.c
	mkdir -p $(dir $@)
	$(COMPILER) $(LIBS) -MM -MT '$(@:.d=.o)' $< -MF $@
##############
####src#######
$(BUILD)/%.o: $(SOURCE_DIR)/%.cpp
	$(COMPILER) $(LIBS) -c $< -o $@
$(BUILD)/%.d: $(SOURCE_DIR)/%.cpp
	mkdir -p $(dir $@)
	$(COMPILER) $(LIBS) -MM -MT '$(@:.d=.o)' $< -MF $@	
$(BINARY): $(OBJS) $(DEPS)
	$(COMPILER) $(OBJS) $(LIBS) -o $(BINARY)
#############
###############
###CLEAN######
clean-dep:
	rm -f $(DEPS)
clean: clean-dep
	rm -f $(OBJS)
distclean: clean
	rm -fr $(BUILD)
##############
####AHBU####
-include $(DEPS)