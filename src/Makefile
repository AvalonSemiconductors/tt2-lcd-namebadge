SIM ?= icarus
TOPLEVEL_LANG ?= verilog

ifneq ($(GATES),yes)
# normal simulation
VERILOG_SOURCES += $(PWD)/tb.v $(PWD)/toplevel.v $(PWD)/lcd.v
COMPILE_ARGS += -DTESTING
else
# gate level simulation requires some extra setup
COMPILE_ARGS += -DGL_TEST
COMPILE_ARGS += -DFUNCTIONAL
COMPILE_ARGS += -DUSE_POWER_PINS
COMPILE_ARGS += -DSIM
COMPILE_ARGS += -DUNIT_DELAY=#1
VERILOG_SOURCES += $(PDK_ROOT)/sky130B/libs.ref/sky130_fd_sc_hd/verilog/primitives.v
VERILOG_SOURCES += $(PDK_ROOT)/sky130B/libs.ref/sky130_fd_sc_hd/verilog/sky130_fd_sc_hd.v

# gatelevel verilog from /runs/wokwi/results/final/verilog/gl/
VERILOG_SOURCES += $(PWD)/tb.v $(PWD)/tt2_tholin_namebadge.v
endif

# TOPLEVEL is the name of the toplevel module in your Verilog or VHDL file
TOPLEVEL = tb

# MODULE is the basename of the Python test file
MODULE = test

include $(shell cocotb-config --makefiles)/Makefile.sim
