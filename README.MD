06/04/2018:
Micro$oft has acquired github, you can find updates from this software at: https://coto88.bitbucket.io/
Have a good day.

Coto:

This source has been rewritten completely, so I use gnu gpl v2 license.

Notes:
	While reading the source I will use two kinds of indexing (for accessing File Descriptor contexts): 
		- One being POSIX compliant (struct dirent)
		
		- Internal struct fd 
		(an extension of the above struct that abstracts/wraps enough data to allow FSFAT driver to co-operate with newlib)
		
Changes:

- implemented properly the (ino_t d_ino) attribute required for struct dirent, and we use it as the Internal struct fd index
	(so we can access the struct stat from dirent directly for file/dir attribute handling, without having to call fsfat layer repeteadly,
	so we reuse the POSIX implementation for built-in read/file parse, and unless strictly necessary, use fsfat layer for specifics).

- Rewritten most of the code, removed some (imo) redundant stuff, and merged functions to improve readibility (for the code and the user!)

- implemented POSIX open/read/write/close through a devoptab(dirent.h,etc), 
	the current toolchain (yet to be released) is based on libc nano, and wipes completely posix filesystem support so we restore that.
