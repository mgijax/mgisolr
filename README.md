The mgisolr product includes:
1. the definitions for the various Solr indexes supporting the MGI web site
2. knowledge of how to take those definitions and build the necessary directory hierarchies for the fe, snp, and gxd Solr servers

It assumes:
- the Solr executable resides elsewhere in the file system

Currently supported Solr version is 8.5.3.

To add support for a new Solr instance (named `x`, for instance):
1. Go into the `sets/` directory.
2. Create a new `x.indexes` file.  It can be empty at first.  It will have one index (core) name on each line when you add indexes.
3. Create a new `x.solr.xml` file to define its Solr configuration.  This can likely just be a copy of `fe.solr.xml`.

To add a new Solr index (adding index `y` to Solr instance `x`, for instance):
1. Open `sets/x.indexes`.
2. Add a new line with `y` on it.
3. Go into the `cores/` directory.
3. Create a new directory `y` for the index.
4. It is easiest to copy an existing simple core, so `cp authorsAC/* y`.
5. Edit `y/core.properties` to set the name of the new core to be `y`.
6. Edit `y/schema.xml` and go to the bottom where the customizations for each index live.
7. Add &lt;fieldType&gt; and &lt;field&gt; definitions as needed.
8. Add &lt;copyField&gt; definitions if needed.
9. Ensure &lt;uniqueKey&gt; is set properly.
