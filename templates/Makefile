SDK_VERSION ?= v1.1.0-pre0

bump-versions: bump-go-versions bump-rust-versions

bump-go-versions:
	@for dir in $$(ls -d *-go) ; do \
		cd $$dir/content ; \
		sed -i.sed-bak -e 's%require github.com/fermyon/spin/sdk/go v.*%require github.com/fermyon/spin/sdk/go ${SDK_VERSION}%g' go.mod ; \
		sed -i.sed-bak -e 's/{{project-name | snake_case}}/foo/g' go.mod ; \
		go mod tidy ; \
		sed -i.sed-bak -e 's/foo/{{project-name | snake_case}}/g' go.mod ; \
		rm *.sed-bak ; \
		cd - 2>&1 >/dev/null ; \
	done

bump-rust-versions:
	@for dir in $$(ls -d *-rust) ; do \
		cd $$dir/content ; \
		sed -i.sed-bak -e 's%"https://github.com/fermyon/spin", tag = "v.*"%"https://github.com/fermyon/spin", tag = "${SDK_VERSION}"%g' Cargo.toml ; \
		rm *.sed-bak ; \
		cd - 2>&1 >/dev/null ; \
	done
