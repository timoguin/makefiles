#==============================================================================
define INFO

name:    Terraform module Makefile wrapper
version: 0.1.0
author:  timoguin@gmail.com
git:     https://github.com/timoguin/makefiles//terraform-module-testing/Makefile

endef
export INFO

.PHONY : all default help info lint test
#==============================================================================


default : help

all : lint test ## Run test suite

lint : ## Lint the Terraform code (currently only runs fmt)
	make -f tests/Makefile fmt ${args}

test : ## Run all integration tests in the tests/ directory
	cd tests && make clean && make test

help : ## Show help for available targets
	@echo "Available commands:"
	@echo
	@cat Makefile* | grep -E '^[a-zA-Z_-]+ ?:.*?## .*$$' | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36mmake %-30s\033[0m %s\n", $$1, $$2}'
	@echo

info : ## Show metadata info about this Makefile
	@echo "Makefile metadata:"
	@echo "$$INFO"
