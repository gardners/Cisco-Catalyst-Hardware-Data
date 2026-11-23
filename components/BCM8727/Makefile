DOC=BCM8727_Open_Source_Datasheet
.PHONY: all clean
all: $(DOC).pdf
$(DOC).pdf: $(DOC).tex
	pdflatex -interaction=nonstopmode -halt-on-error $(DOC).tex
	pdflatex -interaction=nonstopmode -halt-on-error $(DOC).tex
clean:
	rm -f $(DOC).aux $(DOC).log $(DOC).out $(DOC).toc
