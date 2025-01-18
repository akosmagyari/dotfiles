# Directory structure
SVG_DIR := svg
ICO_DIR := ico

# Tools
SVGEXPORT := svgexport
PNG2ICO := png2ico

# File lists
SVG_FILES := $(wildcard $(SVG_DIR)/*.svg)
ICO_FILES := $(patsubst $(SVG_DIR)/%.svg,$(ICO_DIR)/%.ico,$(SVG_FILES))

# Standard ICO sizes (all widths are multiples of 8 and <256)
SIZES := 16 24 32 48 64 128 248

# Default target
all: $(ICO_FILES)

# Create ICO directory if it doesn't exist
$(ICO_DIR):
	mkdir -p $(ICO_DIR)

# Rule to convert SVG to ICO
$(ICO_DIR)/%.ico: $(SVG_DIR)/%.svg | $(ICO_DIR)
	@echo "Converting $< to ICO..."
	@# Create temporary PNGs at different sizes
	@for size in $(SIZES); do \
		$(SVGEXPORT) $< $*_$${size}.png $${size}:$${size}; \
	done
	@# Combine PNGs into ICO
	@$(PNG2ICO) $@ $(foreach size,$(SIZES),$*_$(size).png)
	@# Clean up temporary PNG files
	@rm -f $(foreach size,$(SIZES),$*_$(size).png)
	@echo "Created $@"

# Clean target
clean:
	rm -rf $(ICO_DIR)
	rm -f *.png

.PHONY: all clean
