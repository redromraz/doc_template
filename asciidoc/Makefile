INPUTDIR = $(CURDIR)
DOCKERIMG=asciidoctor/docker-asciidoctor
ASCIIDOCTOR=docker run --rm -it -v $(INPUTDIR):$(INPUTDIR) -w $(INPUTDIR) $(DOCKERIMG) asciidoctor

.PHONY: all
all: out.html

out.html:
	@$(ASCIIDOCTOR) \
		--out-file=$(INPUTDIR)/out.html \
		$(wildcard *.adoc)
