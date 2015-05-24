AC_INIT([gputools], 0.3)
AC_CONFIG_AUX_DIR([tools])

AC_MSG_CHECKING("CUDA compiler")
AC_ARG_WITH([nvcc],
  AC_HELP_STRING([--with-nvcc=nvcc],
    [specify a CUDA compiler, e.g. /usr/local/cuda/bin/nvcc]),
    [NVCC="$withval"])
if test -z "${NVCC}"; then
  AC_MSG_RESULT("environment variable NVCC not set")
  AC_CHECK_PROG([NVCC], [nvcc], [/usr/local/cuda/bin/nvcc])
fi
CUDA_BIN_DIR=`AS_DIRNAME(["$NVCC"])`
AC_MSG_RESULT("using NVCC=${NVCC}")

AC_MSG_CHECKING("root of the CUDA install directory")
AC_ARG_WITH([cuda],
  AC_HELP_STRING([--with-cuda=cuda],
    [specify the root of your cuda install, e.g. /usr/local/cuda]),
    [CUDA_HOME="$withval"])
if test -z "${CUDA_HOME}"; then
  AC_MSG_RESULT("environment variable CUDA_HOME not set")
  CUDA_HOME=`AS_DIRNAME(["$CUDA_BIN_DIR"])`
fi
AC_MSG_RESULT("using CUDA_HOME=${CUDA_HOME}")

AC_MSG_CHECKING("location of CUDA libraries")
AC_CHECK_FILE(["${CUDA_HOME}/lib/libcublas.so"],[CUDA_LIB="${CUDA_HOME}/lib"],[CUDA_LIB=""])
if test -z "${CUDA_LIB}"; then
  AC_CHECK_FILE(["${CUDA_HOME}/lib64/libcublas.so"],[CUDA_LIB="${CUDA_HOME}/lib64"],[CUDA_LIB=""])
fi
if test -z "${CUDA_LIB}"; then
  AC_CHECK_FILE(["${CUDA_HOME}/lib/libcublas.dylib"],[CUDA_LIB="${CUDA_HOME}/lib"],[CUDA_LIB=""])
fi
if test -z "${CUDA_LIB}"; then
  AC_CHECK_FILE(["${CUDA_HOME}/lib64/libcublas.dylib"],[CUDA_LIB="${CUDA_HOME}/lib64"],[CUDA_LIB=""])
fi

AC_MSG_CHECKING("R")

AC_ARG_WITH([r],
  AC_HELP_STRING([--with-r=r],
    [specify the full path to the root of the R install directory, e.g. /usr/lib64/R]),
    [R_HOME="$withval"])
if test -z "${R_HOME}"; then
  : ${R_HOME=`R RHOME`}
  if test -z "${R_HOME}"; then
    echo "could not determine R_HOME"
    exit 1
  fi
fi
AC_MSG_RESULT("using ${R_HOME} for the root of the R install directory")

AC_ARG_WITH([r-include],
  AC_HELP_STRING([--with-r-include=r_include],
    [specify the full path to your R header files, e.g. /usr/share/R/include]),
    [R_INCLUDE="$withval"])
if test -z "${R_INCLUDE}"; then
  R_INCLUDE="${R_HOME}/include"
fi
AC_MSG_RESULT("using ${R_INCLUDE} for R header files")

AC_ARG_WITH([r-lib],
  AC_HELP_STRING([--with-r-lib=r-lib],
    [specify the full path to your R shared libraries, e.g. /usr/lib64/R/lib]),
    [R_LIB="$withval"])
if test -z "${R_LIB}"; then
  R_LIB="${R_HOME}/lib"
fi
AC_MSG_RESULT("using ${R_LIB} for R shared libraries")

CC=`"${R_HOME}/bin/R" CMD config CC`
CFLAGS=`"${R_HOME}/bin/R" CMD config CFLAGS`
CPPFLAGS=`"${R_HOME}/bin/R" CMD config CPPFLAGS`
CPICFLAGS=`"${R_HOME}/bin/R" CMD config CPICFLAGS`

LDFLAGS=`"${R_HOME}/bin/R" CMD config LDFLAGS`

AC_SUBST(NVCC)
AC_SUBST(CUDA_HOME)
AC_SUBST(CUDA_LIB)

AC_SUBST(R_HOME)
AC_SUBST(R_INCLUDE)
AC_SUBST(R_LIB)

AC_SUBST(CC)
AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(CPICFLAGS)

AC_SUBST(LDFLAGS)

AC_CONFIG_FILES([src/Makefile])
AC_OUTPUT