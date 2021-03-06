######################################################################
#
#	make all
#		Run all Python tests.
#
#	make clean
#		Remove compiled Python files and output.
#
#######################################################################

PYTHON = python

SHELL=/bin/sh

.PHONY: all clean

EXAMPLES = \
	ClassInterface/ClassExample.py \
	ClassInterface/WindowExample.py \
	GlobalSpectralAnalysis/SHComplexSpectralAnalysis.py \
	GlobalSpectralAnalysis/SHRealSpectralAnalysis.py \
	IOStorageConversions/SHConversions.py \
	IOStorageConversions/SHStorage.py \
	LocalizedSpectralAnalysis/SHMultitaperSE.py \
	LocalizedSpectralAnalysis/SHWindowsBiasOther.py \
	SHRotations/SHRotations.py \
	GravMag/TestGrav.py \
	GravMag/TestCT.py \
	Other/TestOther.py \
	TestLegendre/TestLegendre.py \
	TimingAccuracy/TimingAccuracyDH.py \
	TimingAccuracy/TimingAccuracyDHC.py \
	TimingAccuracy/TimingAccuracyGLQ.py \
	TimingAccuracy/TimingAccuracyGLQC.py \
	$(EMPTY)

define run-example
# Create a phony rule to run each example.
$(addsuffix .phony,$1):
	cd $(dir $1) ; $(PYTHON) ./$(notdir $1)

.PHONY: $(addsuffix .phony,$1)
endef

$(foreach example,$(EXAMPLES),$(eval $(call run-example,$(example))))

all: $(addsuffix .phony, $(EXAMPLES))

clean:
	-rm -rf Common/*.pyc Common/__pycache__/
	-rm -f $(addsuffix *.pyc, $(dir $(EXAMPLES)))
	-rm -rf $(addsuffix __pycache__, $(dir $(EXAMPLES)))
	-rm -f $(addsuffix *.png, $(dir $(EXAMPLES)))
