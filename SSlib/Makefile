###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

HOME = /Users/sahara
VPPHOME = /Applications/"TheVDM++Toolbox"
VPPDE = $(VPPHOME)/bin/vppde
#VPPDE = ~/bin/vppde

#encode
#CODE = SJIS
CODE = UTF8

# TeX commands
TEXDIR = /usr/local/texlive/2016/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex --kanji=$(C0DE)
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = SSlib

# VPP files
VPPFILES0 = AllT.vpp

VPPFILES1 = Calendar.vpp Character.vpp CommonDefinition.vpp \
	Control.vpp \
	Date.vpp DoubleListQueue.vpp Function.vpp Hashtable.vpp \
	Integer.vpp JapaneseCalendar.vpp Map.vpp Number.vpp \
	Object.vpp Product.vpp Queue.vpp Real.vpp SBCalendar.vpp \
	Sequence.vpp Set.vpp String.vpp Term.vpp Time.vpp UniqueSequence.vpp \
	CalendarT.vpp ControlT.vpp DateT.vpp \
	DoubleListQueueT.vpp FunctionT.vpp \
	HashtableT.vpp IntegerT.vpp MapT.vpp \
	NumberT.vpp ProductT.vpp QueueT.vpp Queue4Tread.vpp \
	RealT.vpp SBCalendarT.vpp SequenceT.vpp \
	SetT.vpp StringT.vpp TermT.vpp \
	TestCase.vpp TestDriver.vpp TestLogger.vpp \
	TimeT.vpp UniqueSequenceT.vpp \
	./stdlib/io.vpp ./stdlib/math.vpp ./stdlib/VDMUtil.vpp

# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  testAndPDF
#	makepdf $(OUTDOC) utf8
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
	makeindex  $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# run VDMTools and Pretty print
testAndPDF:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES0) $(VPPFILES1)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES0) $(VPPFILES1)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES0) $(VPPFILES1)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES0) $(VPPFILES1)

# run VDMTools
vdmtools:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES0) $(VPPFILES1)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES0) $(VPPFILES1)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES0) $(VPPFILES1)
	
# run VDMJ
vdmj:
	echo $(CODE)
	vdmj_UTF8 -exceptions -e "run()" $(VPPFILES0) $(VPPFILES1)

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc
	rm -rf image/*.bb

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf
