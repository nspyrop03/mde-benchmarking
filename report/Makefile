TARGET = report

XELATEX = xelatex --shell-escape $(TARGET).tex
BIBER = biber $(TARGET)

.PHONY: all quick
all: quick

quick:
	$(XELATEX)
	@echo "Quick build complete."

.PHONY: full
full:
	$(XELATEX)
	$(BIBER)
	$(XELATEX)
	$(XELATEX)
	@echo "Full build complete."

.PHONY: clean
clean:
	rm -f $(TARGET).aux $(TARGET).bbl $(TARGET).bcf $(TARGET).blg $(TARGET).log $(TARGET).out $(TARGET).run.xml $(TARGET).toc $(TARGET).pdf
