# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line.
SPHINXOPTS    =
SPHINXBUILD   = sphinx-build
SPHINXPROJ    = nhanssite
SOURCEDIR     = .
BUILDDIR      = _build

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	rm -Rf $(BUILDDIR)/html/* 
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

	# clearn root githubpage document
	rm -Rf $(BUILDDIR)/../../docs/*

	# cp nesscacery files
	cp -rf $(BUILDDIR)/../docs_template/* $(BUILDDIR)/../../docs/

	# cp html files
	cp -rf $(BUILDDIR)/html/* $(BUILDDIR)/../../docs/