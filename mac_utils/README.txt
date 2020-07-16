This folder contains utilities to help building and debugging
binaries: 

- int: uses `install_name_tool` to transform all dependencies
  specified as absolute paths into relative paths, if the dependency
  is present in the same folder
- my-ldd: works similar to linux' ldd, tries loading all specified
  dependencies, notifies of failures
