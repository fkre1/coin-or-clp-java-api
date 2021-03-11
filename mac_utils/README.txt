This folder contains utilities to help building and debugging
binaries:

- make_rpaths: uses `install_name_tool` to transform all dependencies
  specified as absolute paths into relative paths, if the dependency
  is present in the same folder; also changes library IDs and rpaths
- mac-ldd: works similar to linux' ldd, tries loading all specified
  dependencies, notifies of failures; used for debugging missing dependencies
