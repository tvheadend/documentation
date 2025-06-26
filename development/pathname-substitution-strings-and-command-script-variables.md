# Pathname Substitution Strings and Command Script Variables

TVH has the ability to build a recording file and path name using predefined substitution strings. For example, using `$t` will include the EPG Title in the file name. Likewise, `%t` will pass the EPG Title as a command line argument to one of the DVR Profile command scripts.

This feature is implemented in `src/dvr/dvr_rec.c`.

A number of `htsstr_substitute_t` arrays contain a list of substitution identifiers and the functions required to perform the required substitution.

The actual substitution is performed by `htsstr_substitute` (`src/htsstr.c`) which is passed a substitution array and a substitution key (`$` or `%`) as well as an output variable.

Pathname substitution strings can be applied equally to the file name and to directories in the hierarchy under the base directory specified in the DVR Profile. It should be noted, however, that objects that can provide their own directories, such as AutoRec and Timer DVR objects, must have their directory prefixed with `$$` for substitutions to take place. The `$$` prefix will be omitted from the final directory name.
