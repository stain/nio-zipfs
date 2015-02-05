# nio-zipfs

[ZipFileSystem](src/main/java/no/s11/zipfs/ZipFileSystem) 
is a file system provider that treats the contents of a zip or
JAR file as a [java.nio.file.FileSystem](http://docs.oracle.com/javase/7/docs/api/java/nio/file/FileSystem.html).

# Building

To build, you will need Oracle JDK 7/OpenJDK 7 or newer, 
together with [Apache Maven 3.x](http://maven.apache.org/download.html). 

This implementation is tested with Maven 3.2, openjdk7 and openjdk8.

To build:

	mvn clean install

To then use from a Maven project, use:

	<dependency>
		<groupId>no.s11.zipfs</groupId>
		<artifactId>nio-zipfs</artifactId>
		<version>8.60.0-SNAPSHOT</version>	
	</dependency>
	
Check [pom.xml](pom.xml) to find the latest `<version>` number.	

TODO: Set up Maven snapshot repository.


# Usage

The factory methods defined by the 
[java.nio.file.FileSystems](http://docs.oracle.com/javase/7/docs/api/java/nio/file/FileSystems.html) 
class can be used to create a `FileSystem`, e.g:

	   // use file type detection
	   Path jarfile = Paths.get("foo.jar");
	   FileSystem fs = FileSystems.newFileSystem(jarfile, null);

-or-:

	   // locate file system by the legacy JAR URL syntax
	   Map<String,?> env = Collections.emptyMap();
	   URI uri = URI.create("zip:file:/mydir/foo.jar");
	   FileSystem fs = FileSystems.newFileSystem(uri, env);

Once a FileSystem is created then classes in the 
[java.nio.file package](http://docs.oracle.com/javase/7/docs/api/java/nio/file/package-summary.html)
can be used to access files in the zip/JAR file, eg:

	   Path mf = fs.getPath("/META-INF/MANIFEST.MF");
	   InputStream in = mf.newInputStream();

See [Demo.java](src/test/java/no/s11/zipfs/Demo.java) for more interesting usages.


# License

**License**: [BSD 3-Clause](http://opensource.org/licenses/BSD-3-Clause)

- Copyright (c) 2015 University of Manchester, UK.
- Copyright (c) 2009, 2012, Oracle and/or its affiliates. 

All rights reserved.  

Based on the zipfs demo of OpenJDK 8 by Oracle, distributed
under a [BSD 3-Clause license](LICENSE).


## Relation to OpenJDK

This code is based on the 
[demo/nio/zipfs](http://hg.openjdk.java.net/jdk8u/jdk8u/jdk/file/c10fd784956c/src/share/demo/nio/zipfs) 
code from [OpenJDK 8](http://openjdk.java.net/projects/jdk8/) which has been distributed
with Open JDK since 7u20.

While OpenJDK 8 is licensed under 
[GPL 2 with the classpath exception](http://openjdk.java.net/legal/gplv2+ce.html),
the zipfs code was 
[distributed under the BSD 3-Clause license](http://hg.openjdk.java.net/jdk8u/jdk8u/jdk/file/c10fd784956c/src/share/demo/nio/zipfs/src/com/sun/nio/zipfs/ZipFileSystemProvider.java#l2).

Since OpenJDK 9, 
[zipfs is included in the main OpenJDK codebase](http://hg.openjdk.java.net/jdk9/dev/jdk/file/b8e8497c541c/src/jdk.zipfs/share/classes/jdk/nio/zipfs), 
but now covered by the GPL license.

This code in *nio-zipfs* is only based on the OpenJDK 8 demo code,
and remains licensed under BSD 3-Clause, which makes it compatible with 
other open source licenses like Apache Software License 2.0,
provided you retain the notices in the files [NOTICE](NOTICE) and [LICENSE](LICENSE).  



