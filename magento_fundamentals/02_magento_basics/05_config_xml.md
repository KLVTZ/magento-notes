Configuration XML
=================

This is where we register our module. Magento configuration is a bunch of XML
files merged together into one tree. If the application is initialized, then we
look in `app/etc/modules`, we have module registration files or activation
files. The code that actually looks in here just globs and is read. It's not
enough to rename the file, if it is in XML, it will be read.

What they look like internally is a root node. For configuration, it is config.
In it you will have modules tag as well as module name.

```xml
<config>
	<modules>
		<Enterprise_Banner>
			<active>true</active>
			<codePool>core</codePool>
			<depends>
				<Mage_Adminhtml/>
				<Mage_CatalogRule/>
				<Mage_SalesRule/>
				<Enterprise_Cms/>
				<Enterprise_CustomerSegment/>
			</depends>
		</Enterprise_Banner>
	</modules>
</config>
```

For this setting, this is in core, we go to `app/code/core/Enterprise/Banner.

Global node
------------
Configuration files are all merged into one. All those XML files. Base on what
we find under our config modules, we will look for `etc/` folder in each
director. Machine looks at that bit path and gets that information. One thing to
note is that each file is loaded in alphabetical order. 

- main database settings, such as host, databasem name, user,
	name, password, and some system values. These can be found in the system
- Connecction types (read/write). 
- Database adapter.
- Core module class names are configured.

*/etc/config.xml*

Default node
-------------
- Directory structure real folder names
- System local
- Design and Theme configuration
- System options.

Nodes in config are important. These are configuration areas that are different
from the design areas.

Frontend node
-------------
- Routers
- Translation files
- Layout XML files
- Observers declarations -event driven architecture


Catalog node
------------
Specific to a certain module. When those values are retrieve, you may have a
system config that has values to. But remember that the system config would
overtake the settings in config.

```xml
<config>
	<modules>
		<!-- Contains modules declarations(names, statuses, dependencies) -->
	</modules>
	<global>
		<!-- Contains definitions that should be shares between all scopes -->
	</global>
	<default>
		<!-- Contains definitions shared between all stores configuration -->
	</default>
	<frontend>
		<!-- Contains definitions that require only for frontend area -->
	</frontend>
	<catalog>
		<!-- Contains declarations that require only for Mage_Catalog_module -->
	</catalog>
</config>
```

How to access configuration value
---------------------------------

- To get part of config: `$store->getConfig($path);`
- To get part of config: `Mage::getStoreConfig($path, [, $store]);`
- To check store flag: `Mage::getStoreConfigFlag($path, [, $store]);`
- To access by absolute path: `Mage::getConfig()->getNode($path, [, $scope]);`

Store's Area Responsibilities
-----------------------------

- Website -> Design defaults, Locale, defaults
- Store Group -> Root Category
- Store -> Design, Locale


