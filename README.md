# Package #

Go bindings for libhdfs v2, for manipulating files on Hadoop distributed file system.

# Types #

- `hdfs.Fs`: file system handle
- `hdfs.File`: file handle
- `hdfs.FileInfo`: file metadata structure, represented within Go

# Methods #

see `go doc`

# Usage #

## Prerequisite ##

- JVM
- HDFS: c bindings for libhdfs v2, java binary packages
- HDFS: configured cluster (localhost or edit the server= variable in tests)

## Test ##

Assuming you have HDFS running on localhost:56565

		export CLASSPATH=$(find $HADOOP_HOME -name *.jar | tr \\n : ):$JAVA_HOME/jre/lib/rt.jar 
		export LD_LIBRARY_PATH="$HADOO_HOME/lib/native/:$JAVA_HOME/jre/lib/amd64/server/" 
		export CGO_CFLAGS="-I/usr/include/ -I$HADOOP_HOME/include" 
		export CGO_LDFLAGS="-L $HADOOP_HOME/lib/native -L $JAVA_HOME/jre/lib/amd64/server/"
		go test


# Known Issues #

1. `errno` in libhdfs is not handled precisely. For example, `invokeMethod()` would probably sets `errno` to **2** in a lot of routines.
1. O\_APPEND not working correctly on libhdfs v2
