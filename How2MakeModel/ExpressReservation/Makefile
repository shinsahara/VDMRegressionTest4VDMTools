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
OUTDOC = ExpressReservation

# VDM files
VPPFILES = \
Card.vpp			ExpressReservatiopn.vpp		Wallet.vpp \
Common.vpp			 Contract.vpp			MyTest.vpp		MyTestCase.vpp		 \
CredirCard.vpp			ReservationDomain.vpp \
CustomerCard.vpp		ReservationSysytem.vpp ReservationDomainData.vpp

UTILITYFILES = \
	../Utilities/Character.vpp	../Utilities/Sequence.vpp	../Utilities/String.vpp \
	../stdlib/io.vpp	../Utilities/VDMUnit.vpp	../stdlib/VDMUtil.vpp

# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  testAndPDF
	ebb image/*.jpg
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
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc *.lot *.lof

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf