###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

HOME = /Users/sahara
VPPHOME = $(HOME)/vdmpp
VPPDE = $(VPPHOME)/bin/vppde

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
OUTDOC = VPP-Intro

# VDM files
VPPFILES = $(VPPFILES0) $(VPPFILES1) $(VPPFILES2) $(RQFILE) $(UTILITYFILES)

VPPFILES0 = \
	BLogic/Library0.vpp	ReqDict/Library0RQ1.vdmpp
		
VPPFILES1 = \
	BLogic/Library1.vpp \
	Test/MyTest.vpp		Test/MyTestCase.vpp 
	
VPPFILES2 = \
	BLogic/Library2.vpp \
	ReqDict/Author2.vdmpp	ReqDict/Book2.vpp \
	ReqDict/BookStacks.vdmpp ReqDict/Field2.vdmpp \
	ReqDict/Lend2.vdmpp ReqDict/Person2.vdmpp ReqDict/Staff2.vdmpp ReqDict/User2.vdmpp \
	Test/MyTest2.vpp	Test/MyTestCase2.vpp

RQFILE = \
	ReqDict/LibraryRQ1.vdmpp 
	
UTILITYFILES = \
	../Utilities/Character.vpp	../Utilities/Sequence.vpp	../Utilities/String.vpp \
	../stdlib/io.vpp	../Utilities/VDMUnit.vpp	../stdlib/VDMUtil.vpp
	
# Test script name
TESTSCRIPT = test.script
TESTSCRIPT2 = test2.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  testAndPDF
#$(OUTDOC): 
#	$(PLATEX) $(OUTDOC)
#	$(BIBTEX) $(OUTDOC)
#	makeindex $(OUTDOC).idx
#	$(PLATEX) $(OUTDOC)
#	$(PLATEX) $(OUTDOC)
#	$(DVIPDFM) $(OUTDOC)

# run VDMTools and Pretty print
testAndPDF:
	rmvdmtc.sh
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm1.tc $(TESTSCRIPT) $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	#	
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm2.tc $(TESTSCRIPT2) $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# merge test coverage data
	mergetc vdm1.tc vdm2.tc > vdm.tc
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES)


# run VDMTools
vdmtools:
	rmvdmtc.sh
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm1.tc $(TESTSCRIPT) $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	#	
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm2.tc $(TESTSCRIPT2) $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
	# merge test coverage data
	mergetc vdm1.tc vdm2.tc > vdm.tc

# run VDMJ
vdmj:
	vdmj_UTF8 -r classic -exceptions -e "run()" -default "TestApp" $(VPPFILES1)  $(RQFILE) $(UTILITYFILES)
	vdmj_UTF8 -r classic -exceptions -e "run()" -default "TestApp2" $(VPPFILES2)  $(RQFILE) $(UTILITYFILES)

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf