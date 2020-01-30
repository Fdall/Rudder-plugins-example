PLUGIN_NAME="mydemo_plugin"
VERSION="6.0-1.0"

$(PLUGIN_NAME)-$(VERSION).rpkg: target/metadata target/files.txz target/scripts.txz
	ar r $(PLUGIN_NAME)-$(VERSION).rpkg target/metadata target/files.txz target/scripts.txz

target/metadata:
	mkdir -p target
	cp packaging/metadata target/metadata
	sed -i -e "s/\$${plugin-version}/$(VERSION)/g" target/metadata
	sed -i -e "s/\$${plugin-name}/$(PLUGIN_NAME)/g" target/metadata

target/scripts.txz:
	mkdir -p target/packaging
	cp -r packaging target/
	wget -O target/packaging/rudder-synchronize https://repository.rudder.io/tools/rudder-synchronize
	tar cJ -C packaging -f target/scripts.txz target/packaging

target/files.txz:
	mkdir -p target/configuration
	cp -r configuration/ncf/30_generic_methods target/configuration/
	tar cJ -C target -f target/files.txz target/configuration

clean:
	rm -f $(PLUGIN_NAME)-*.rpkg
	rm -rf target
