The mgisolr product includes:
1. the definitions for the various Solr indexes supporting the MGI web site
2. knowledge of how to take those definitions and build the necessary directory hierarchies for the fe, snp, and gxd Solr instances

It assumes:
- The directory containing the Solr instance is defined in SOLR_HOME.
- The currently supported Solr version is 8.5.2.

To add support for a new Solr instance (named `x`, for instance):
1. Go into the `sets/` directory.
2. Create a new `x.indexes` file.  It can be empty at first.  It will have one index (core) name on each line when you add indexes.
3. Create a new `x.solr.xml` file to define its Solr configuration.  This can likely just be a copy of `fe.solr.xml`.
3. Create a new `x.ram` file to define how much RAM to devote to Solr.  (This sets both -Xms and -Xms for the JVM.)

To add a new Solr index (adding index `y` to Solr instance `x`, for instance):
1. Open `sets/x.indexes`.
2. Add a new line with `y` on it.
3. Go into the `cores/` directory.
3. Create a new directory `y` for the index.
4. It is easiest to copy an existing simple core, so `cp authorsAC/* y`.
5. Edit `y/core.properties` to set the name of the new core to be `y`.
6. Edit `y/schema.xml` and go to the bottom where the customizations for each index live.
7. Remove the old &lt;fieldType&gt;, &lt;field&gt;, and &lt;copyField&gt; definitions.
7. Add &lt;fieldType&gt; and &lt;field&gt; definitions as needed.
8. Add &lt;copyField&gt; definitions if needed.
9. Ensure &lt;uniqueKey&gt; is set properly.

To build a new installation for instance `x` under directory `a`, named as subdirectory `b`, and running on port `c`:
1. Set your SOLR_HOME environment variable to the installation directory for Solr itself.
2. Go into your `mgisolr/` directory.
3. Run `./buildInstance x c a b`.
4. At that point, you can `cd a/b` and then run `./startSolr.sh`

To apply updated index definitions to an instance of `x` that lives in directory `d` and NOT erase the contents of those directories (so you can re-index a single core and leave the others as-is):
1. Set your SOLR_HOME environment variable to the installation directory for Solr itself.
2. `cd d`
3. Run `./stopSolr.sh`
4. Go into your `mgisolr/` directory.
5. Run `./rebuildInstance x d`.
6. At that point, you can `cd d` and then run `./startSolr.sh`

To completely rebuild a new installation for instance `x` under directory `a`, named as subdirectory `b`, and running on port `c` (leaving empty indexes):
1. Set your SOLR_HOME environment variable to the installation directory for Solr itself.
2. Go into your `mgisolr/` directory.
3. Run `./buildInstance x c a b replace`.
4. At that point, you can `cd a/b` and then run `./startSolr.sh`
