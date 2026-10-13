# Ensembl Bacteria release containing the annotation file.
ENSEMBL_RELEASE := 63
# Ensembl directory name for this Salmonella enterica strain.
SPECIES := salmonella_enterica_subsp_enterica_serovar_typhimurium_str_lt2_gca_000006945
# Genome assembly identifier used in the annotation filename.
ASSEMBLY := ASM694v2
# Name of the compressed GTF gene annotation file on the Ensembl server.
GTF_NAME := Salmonella_enterica_subsp_enterica_serovar_typhimurium_str_lt2_gca_000006945.$(ASSEMBLY).$(ENSEMBL_RELEASE).gtf.gz
# Full URL assembled from the release, species directory, and filename above.
GTF_URL := https://ftp.ensemblgenomes.ebi.ac.uk/pub/bacteria/release-$(ENSEMBL_RELEASE)/gtf/bacteria_14_collection/$(SPECIES)/$(GTF_NAME)
# Local directory where the downloaded annotation will be saved.
DATA_DIR := data
# Local path of the downloaded GTF file.
GTF_FILE := $(DATA_DIR)/$(GTF_NAME)

# These targets are actions, not files with the same names.
.PHONY: all clean

# Default target: make the GTF file the project needs.
all: $(GTF_FILE)

# Download the GTF only if it is not already present.
$(GTF_FILE):
# Create the output directory if it does not exist yet.
	mkdir -p "$(DATA_DIR)"
# Download to a temporary file first, then rename it after success so an
# interrupted download cannot be mistaken for the complete GTF file.
	@set -eu; \
		tmp="$@.part"; \
		trap 'rm -f "$$tmp"' 0; \
		curl --fail --location --retry 3 --output "$$tmp" "$(GTF_URL)"; \
		mv "$$tmp" "$@"; \
		trap - 0

# Remove the downloaded annotation file.
clean:
	rm -f "$(GTF_FILE)"
