# Require a somewhat recent version of autoconf
AC_PREREQ(2.59)

# Set up package name, version, and bug-reports email
# These can later be referenced in the code as PACKAGE_VERSION,... and
# in the Makefile.am as VERSION
#
AC_INIT(lib_mysqludf_str, 0.3, dtrebbien@gmail.com)

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR(config)

m4_include(config/ax_lib_mysql.m4)

# Initialize automake
AM_INIT_AUTOMAKE

# We need the libtool program
#
AC_PROG_LIBTOOL

# I need a C compiler; C++ projects should use:  AC_PROG_CPP
#
AC_PROG_CC

AC_ARG_WITH(max_random_bytes,
		AC_HELP_STRING([--with-max-random-bytes=INT], [Set the maximum number of bytes that can be generated with a single call to str_srand @<:@4096@:>@]),, [with_max_random_bytes=4096])

AC_DEFINE_UNQUOTED(MAX_RANDOM_BYTES, [${with_max_random_bytes}LL], [Define to a long long integer constant that is the maximum number of bytes that can be generated with a single call to str_srand])

# Require the mysql library.  This uses the ax_lib_mysql.m4
# file to look for the mysql_config program and then run it in order
# to set up MYSQL_CFLAGS and MYSQL_LDFLAGS
#
AX_LIB_MYSQL(,,AC_MSG_ERROR("Can't find mysql library" ))

# Create a header file with various HAVE defines that can be used
# in the source for portability conditionals and other things.  This
# line and file are not necessary.  If it is left out, these definitions
# will be added to CFLAGS (ie. -DHAVE_DLOPEN).
#
#****** Note: config.h can CONFLICT with my_config.h.
#
AM_CONFIG_HEADER(config.h)

AC_CHECK_LIB(dl,dlopen,AC_DEFINE(HAVE_DLOPEN,1,[Have dlopen()]))

AC_C_CONST
AC_TYPE_SIZE_T

# Output from the configure script into Makefile
#
AC_OUTPUT(Makefile)
