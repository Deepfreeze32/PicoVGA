#   make clean ... clean
#   make all ... compile TARGET

##############################################################################
# Configuration

# destination filename
#TARGET = boot2

# stack size of one CPU core (should be 4KB to fit into SRAM banks 4 and 5)
STACK_SIZE = 0x1000

# temporary build directory
TEMP = ./build

# Base makefile (to ensure recompilation after change)
MAKEFILE = ./Makefile

# linker script
LDSCRIPT = ./boot_stage2.ld

# CPU
MCU=cortex-m0plus

# CPU Architecture
MARCH=armv6-m

# FPU
FPU=auto

##############################################################################
# Compilation flags

# define MCU
ARCHCFG = -mcpu=${MCU} -march=${MARCH} -mfpu=${FPU} -mfloat-abi=soft

# use ARM instructions
ARCHCFG += -mthumb

# === ASM flags

# MCU
AFLAGS += ${ARCHCFG}

# === C flags

# MCU
CFLAGS += ${ARCHCFG}

# Optimization level
#CFLAGS += -O0	# do no optimization
#CFLAGS += -O1	# optimize minimally
CFLAGS += -O2	# optimize more
#CFLAGS += -O3	# optimize even more (do not use, compilation may be incorrect)
#CFLAGS += -Ofast # optimize for speed (do not use, compilation may be incorrect)
#CFLAGS += -Og -g3 # optimize for debugger (use together with -g0..-g3, level of debugging information)
#CFLAGS += -Os	# optimize for size

# do not use builtin functions (memset)
CFLAGS += -Wl,--build-id=none
#CFLAGS += -fno-builtin

# do not use standard includes
#CFLAGS += -nostdinc

# create separate sections (to enable eliminate unused sections)
CFLAGS += -fdata-sections -ffunction-sections

# use signed char
CFLAGS += -fsigned-char

# do not assume usual definitions
#CFLAGS += -ffreestanding

# do not use exceptions and unwind frames
CFLAGS += -fno-unwind-tables -fno-exceptions

# --specs=nosys.specs ... do not use _exit
#CFLAGS += --specs=nosys.specs

# --specs=nano.specs ... use small library without printf float
#CFLAGS += --specs=nano.specs

# generate debug informations
#CFLAGS += -g3

# === C++ flags

CPPFLAGS = $(CFLAGS) -std=c++14 -Wno-aligned-new -fno-rtti -nostdinc++

# === Linker flags

# Entry point
LDFLAGS += --entry _stage2_boot

# Linker script
LDFLAGS += -Wl,-script=$(LDSCRIPT)

# do not link startup code and libs
LDFLAGS += -Wl,-nostdlib
# LDFLAGS += -Wl,-nostartfiles

# do not use builtin functions (memset)
LDLAGS += -Wl,--build-id=none

# symbol map
LDFLAGS += -Wl,-Map=$(TEMP)/$(BLD).map

# eliminate unused sections
LDFLAGS += -Wl,--gc-sections,--relax

##############################################################################
# Compiler

# compiler base
COMP = arm-none-eabi-

# C compiler name
CC = ${COMP}gcc

# C++ compiler name
CPP = ${COMP}g++

# ASM compiler name
AS = ${COMP}gcc -x assembler-with-cpp

# Linker
LD = ${COMP}gcc

# Object dump
OD = ${COMP}objdump

# Object copy
OC = ${COMP}objcopy

# Names
NM = ${COMP}nm

# Size
SZ = ${COMP}size

##############################################################################
# File list

# list of all source files
ALLSRC = $(ASRC) $(CSRC) $(SRC)

# list of all files without directory and without extension
ALLBASE = $(notdir $(basename $(ALLSRC)))

# list of all object files *.o
ALLOBJ = $(addprefix $(TEMP)/, $(addsuffix .o, $(ALLBASE)))

##############################################################################
# Clear temporary directory (use "make clean")

clean:
	@rm -rf $(TEMP)

##############################################################################
# Compile all (use "make all")

all: createdirs boot2_generic_03h boot2_is25lp080 boot2_usb_blinky boot2_w25q080 boot2_w25x10cl

##############################################################################
# Create temporary directory

createdirs:
	@mkdir -p $(TEMP)

#############################################################################
# Build the boot2_generic_03h target

boot2_generic_03h: createdirs
	$(eval BLD = boot2_generic_03h)
	@$(AS) $(CFLAGS) $(AFLAGS) -c $(BLD).S -o $(TEMP)/$(BLD).o
	@$(OC) -O binary $(TEMP)/$(BLD).o $(TEMP)/$(BLD).elf
	@$(OC) -O ihex $(TEMP)/$(BLD).o $(TEMP)/$(BLD).hex
	@$(OD) -d -S $(TEMP)/$(BLD).o >  $(TEMP)/$(BLD).lst
	@$(NM) -n $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).sym
	@$(SZ) $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).siz

boot2_is25lp080: createdirs
	$(eval BLD = boot2_is25lp080)
	@$(AS) $(CFLAGS) $(AFLAGS) -c $(BLD).S -o $(TEMP)/$(BLD).o
	@$(OC) -O binary $(TEMP)/$(BLD).o $(TEMP)/$(BLD).elf
	@$(OC) -O ihex $(TEMP)/$(BLD).o $(TEMP)/$(BLD).hex
	@$(OD) -d -S $(TEMP)/$(BLD).o >  $(TEMP)/$(BLD).lst
	@$(NM) -n $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).sym
	@$(SZ) $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).siz

boot2_usb_blinky: createdirs
	$(eval BLD = boot2_usb_blinky)
	@$(AS) $(CFLAGS) $(AFLAGS) -c $(BLD).S -o $(TEMP)/$(BLD).o
	@$(OC) -O binary $(TEMP)/$(BLD).o $(TEMP)/$(BLD).elf
	@$(OC) -O ihex $(TEMP)/$(BLD).o $(TEMP)/$(BLD).hex
	@$(OD) -d -S $(TEMP)/$(BLD).o >  $(TEMP)/$(BLD).lst
	@$(NM) -n $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).sym
	@$(SZ) $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).siz

boot2_w25q080: createdirs
	$(eval BLD = boot2_w25q080)
	@$(AS) $(CFLAGS) $(AFLAGS) -c $(BLD).S -o $(TEMP)/$(BLD).o
	@$(OC) -O binary $(TEMP)/$(BLD).o $(TEMP)/$(BLD).elf
	@$(OC) -O ihex $(TEMP)/$(BLD).o $(TEMP)/$(BLD).hex
	@$(OD) -d -S $(TEMP)/$(BLD).o >  $(TEMP)/$(BLD).lst
	@$(NM) -n $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).sym
	@$(SZ) $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).siz

boot2_w25x10cl: createdirs
	$(eval BLD = boot2_w25x10cl)
	@$(AS) $(CFLAGS) $(AFLAGS) -c $(BLD).S -o $(TEMP)/$(BLD).o
	@$(OC) -O binary $(TEMP)/$(BLD).o $(TEMP)/$(BLD).elf
	@$(OC) -O ihex $(TEMP)/$(BLD).o $(TEMP)/$(BLD).hex
	@$(OD) -d -S $(TEMP)/$(BLD).o >  $(TEMP)/$(BLD).lst
	@$(NM) -n $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).sym
	@$(SZ) $(TEMP)/$(BLD).o > $(TEMP)/$(BLD).siz

##############################################################################
# Head dependencies, to recompile C after changing H

ifneq (${MAKECMDGOALS},clean)
-include $(wildcard $(TEMP)/*.d)
endif

##############################################################################
# List of dependencies not creating files

.PHONY: clean all createdirs boot2_generic_03h boot2_is25lp080 boot2_usb_blinky boot2_w25q080 boot2_w25x10cl
