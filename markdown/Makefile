INPUTDIR = $(CURDIR)
IMAGESDIR= $(INPUTDIR)/images
STYLEDIR= $(INPUTDIR)/style
TEXFLAGS= --verbose --number-sections --from=markdown --to=latex --resource-path="$(IMAGESDIR)"
PDFLATEX= docker run --rm -v $(INPUTDIR):$(INPUTDIR)  -w $(INPUTDIR) texlive/texlive pdflatex
PANDOC= docker run --rm -v $(INPUTDIR):$(INPUTDIR)  -w $(INPUTDIR) pandoc/latex

.PHONY: all
all: article_out.pdf beamer_out.pdf

article_out.pdf: article_out.tex
	@$(PDFLATEX) \
		--output-directory=$(INPUTDIR)/logs \
		article_out.tex
	@mv $(INPUTDIR)/logs/article_out.pdf \
		$(INPUTDIR)

beamer_out.pdf: beamer_out.tex
	@$(PDFLATEX) \
		--output-directory=$(INPUTDIR)/logs \
		beamer_out.tex
	@mv $(INPUTDIR)/logs/beamer_out.pdf \
		$(INPUTDIR)

article_out.tex:
	@$(PANDOC) \
		$(TEXFLAGS) \
		--metadata-file="$(STYLEDIR)/article_metadata.yaml" \
		--include-in-header="$(STYLEDIR)/article_preamble.tex" \
		--output="article_out.tex" \
		$(wildcard *.a.md)

beamer_out.tex:
	@$(PANDOC) \
		$(TEXFLAGS) \
		--metadata-file="$(STYLEDIR)/beamer_metadata.yaml" \
		--include-in-header="$(STYLEDIR)/beamer_preamble.tex" \
		--output="beamer_out.tex" \
		$(wildcard *b.md)

.PHONY: clean
clean:
	@rm $(wildcard *out.tex) \
		 $(wildcard *out.pdf) \
		 $(wildcard logs/*)

