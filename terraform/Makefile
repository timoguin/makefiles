#==============================================================================
define INFO

name:    Terraform Makefile wrapper
version: 0.1.1
author:  timoguin@gmail.com
git:     https://github.com/timoguin/makefiles//terraform/Makefile

endef
export INFO
#==============================================================================

# Default args for various targets
user          := local-$(shell echo $$USER-$$HOSTNAME)
clean_args    := plan.tfplan .terraform logs/* *.tfstate *.tfstate*
args          :=
build_args    :=
init_args     := -var 'user=${user}'
fmt_args      :=
validate_args :=
lint_args     :=
plan_args     := -var 'user=${user}' -out=plan.tfplan ${targets}
apply_args    := plan.tfplan
destroy_args  := -var 'user=${user}'
output_args   :=
import_args   := -var 'user=${user}'
unlock_args   :=

.PHONY: default clean test build_clean build init fmt validate lint plan apply destroy output import unlock debug help info
#==============================================================================

default : help

clean : ## Delete Terraform dirs and plans files
	    ##   args     : clean_args
	    ##   defaults : "plan.tfplan .terraform logs/* *.tfstate *.tfstate*"
	rm -rf ${clean_targets}

test : ## Run all tests in the tests directory
	./run_all.sh

build_clean : clean build ## Run clean and build to create all resources

build : init lint plan apply ## Build all the resources

init : ## Initialize Terraform state
	terraform init ${args} ${init_args}

fmt : ## Run terraform fmt recursively
	terraform fmt -diff -recursive ${args} ${fmt_args}

validate : ## Validate syntax and variables
	terraform validate ${args} ${validate_args}

lint : fmt validate ## Lint the Terraform config (fmt and validate)

plan : ## Run a Terraform plan
	terraform plan ${args} ${default_plan_args} ${plan_args}

apply : ## Run a Terraform apply
	terraform apply ${args} ${apply_args}

destroy : ## Destroy Terraform resources
	terraform destroy ${args} ${destroy_args}

output : ## Show Terraform output variables
	@terraform output ${args} ${output_args}

import : ## Import existing resources into Terraform
	terraform import ${args} ${import_args}

unlock : ## Unlock a Terraform remote state lock
	terraform unlock ${id} ${args}

funlock : ## Force unlock a Terraform remote state lock
	terraform force-unlock -force ${id}

debug : ## Show Makefile variables
	@echo "id (used for unlock): ${id}"
	@echo "args: ${args}"
	@echo "init_args: ${init_args}"
	@echo "fmt_args: ${fmt_args}"
	@echo "validate_args: ${validate_args}"
	@echo "plan_args: ${plan_args}"
	@echo "apply_args: ${apply_args}"
	@echo "destroy_args: ${destroy_args}"
	@echo "output_args: ${output_args}"
	@echo "import_args: ${import_args}"
	@echo "user: ${user}"

help : ## Show help for available targets
	@echo "Available commands:"
	@echo
	@cat Makefile* | grep -E '^[a-zA-Z_-]+ ?:.*?## .*$$' | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36mmake %-30s\033[0m %s\n", $$1, $$2}'
	@echo

info : ## Show metadata info about this Makefile
	@echo "Makefile metadata:"
	@echo "$$INFO"
