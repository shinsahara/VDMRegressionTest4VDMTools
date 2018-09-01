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
TEXDIR = /usr/local/texlive/2018/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = How2MakeModel

# VDM files
VPPFILES = \


# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  testAndPDF
#$(OUTDOC): 
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
	makeindex  $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# make sub-directory's documents
testAndPDF:
	cd ExpressReservation; make all
	cd Fare; make all
	cd EvolvedExpressReservation; make all
	cd libraryByMap; make all

# make sub-directory's documents
vdmtools:
	cd ExpressReservation; make vdmtools
	cd Fare; make vdmtools
	cd EvolvedExpressReservation; make vdmtools
	cd libraryByMap; make vdmtools

# make sub-directory's documents
vdmj:
	cd ExpressReservation; make vdmj
	cd EvolvedExpressReservation; make vdmj
	cd Fare; make vdmj
	cd libraryByMap; make vdmj

# Clean files. But Output document is not deleted.
clean:
	cd ExpressReservation;  make clean; cd ..
	cd Fare; make clean; cd ..
	cd EvolvedExpressReservation; make clean; cd ..
	cd libraryByMap; make clean; cd ..
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc
	rm -rf */*.aux  *.lot *.lof

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf