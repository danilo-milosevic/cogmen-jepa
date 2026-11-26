PDF=output/DaniloMilosevic-SIR.pdf

MAIN=main.md
SECTIONS=$(shell find sections -name '*.md' 2>/dev/null)

PANDOC=pandoc

ifeq ($(OS),Windows_NT)
MKDIR=if not exist output mkdir output
else
MKDIR=mkdir -p output
endif
ENGINE=xelatex

all: pdf

pdf: $(PDF)

$(PDF): $(MAIN) $(SECTIONS) include-files.lua
	$(MKDIR)
	$(PANDOC) $(MAIN) \
		-o $(PDF) \
		--pdf-engine=$(ENGINE) \
		--resource-path=.:./figures:../figures \
		--lua-filter=include-files.lua \
		--citeproc