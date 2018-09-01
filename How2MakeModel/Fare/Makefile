###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

#encode
CODE=UTF8
# TeX commands
TEXDIR = /usr/local/texlive/2015/bin/x86_64-darwin
#TEXDIR = /usr/bin  # Ubuntu 10.10
# PLATEX = platex
#PLATEX = dotexshop
PLATEX = $(TEXDIR)/platex --kanji=$(CODE)
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(CODE)
#DVIPDFM = dvipdfmx
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = Fare

# VPP files
VPPFILES = \
	CalcFare.vdmpp			route_search.vdmpp \
	FareTableDic.vdmpp		dijkstra.vdmpp			route_search_by_dijkstra.vdmpp \
	route_search_testspec.vdmpp \
	MyTest.vdmpp			MyTestCase.vdmpp		railway_network_data.vdmpp \
	UseFare.vdmpp			railway_network.vdmpp 

UTILITYFILES = \
	../Utilities/Character.vpp	../Utilities/Sequence.vpp	../Utilities/String.vpp \
	../Utilities/VDMUnit.vpp \
	../stdlib/io.vpp	../stdlib/VDMUtil.vpp

# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  testAndPDF
#	ebb image/*.jpg
#	$(PLATEX) $(OUTDOC)
#	$(BIBTEX) $(OUTDOC)
#	makeindex  $(OUTDOC).idx
#	$(PLATEX) $(OUTDOC)
#	$(PLATEX) $(OUTDOC)
#	$(DVIPDFM) $(OUTDOC)

# run VDMTools and Pretty print
testAndPDF:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p -R vdm.tc $(VPPFILES) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES) $(UTILITYFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES) 


# run VDMTools
vdmtools:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p -R vdm.tc $(VPPFILES) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES) $(UTILITYFILES)

# run VDMJ
vdmj:
	vdmj_UTF8 -r classic -exceptions -e "run()" -default "TestApp" $(VPPFILES) $(UTILITYFILES)

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf
