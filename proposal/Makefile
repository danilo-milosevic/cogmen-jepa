PDF=output/DaniloMilosevic-SIR.pdf

MAIN=main.md
SECTIONS=$(shell find sections -name '*.md' 2>/dev/null)

PANDOC=pandoc
ENGINE=xelatex

all: pdf

pdf: $(PDF)

$(PDF): $(MAIN) $(SECTIONS) include-files.lua
	if not exist output mkdir output
	$(PANDOC) $(MAIN) \
		-o $(PDF) \
		--pdf-engine=$(ENGINE) \
		--resource-path=.:./figures:../figures \
		--lua-filter=include-files.lua \
		--citeproc