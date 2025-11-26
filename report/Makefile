TARGET = ieee_report

XELATEX = xelatex --shell-escape $(TARGET).tex
#BIBER = biber $(TARGET)

# IEEE class use BibTeX
BIBTEX = bibtex $(TARGET)

.PHONY: all quick
all: quick

quick:
	$(XELATEX)
	@echo "Quick build complete."

.PHONY: full
full:
	$(XELATEX)
	$(BIBTEX)
	$(XELATEX)
	$(XELATEX)
	@echo "Full build complete."

.PHONY: clean
clean:
	rm -f $(TARGET).aux $(TARGET).bbl $(TARGET).bcf $(TARGET).blg $(TARGET).log $(TARGET).out $(TARGET).run.xml $(TARGET).toc $(TARGET).pdf
