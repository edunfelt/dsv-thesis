BUILDDIR=build
FILENAME=front
OUTNAME=report

pdf:
	mkdir $(BUILDDIR) -p
	pandoc \
		--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
		--to=latex \
		--output=$(BUILDDIR)/$(OUTNAME).pdf \
		--metadata-file=meta.yaml \
		--defaults=defaults.yaml

