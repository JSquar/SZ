##=======================================================================
###############################################
# COPYRIGHT: See COPYRIGHT.txt                #
# 2015 by MCS, Argonne National Laboratory.   #
###############################################
##=======================================================================

##=======================================================================
##   PLEASE SET THESE VARIABLES BEFORE COMPILING
##=======================================================================

SZPATH = /home/dreistein/opt/spack/opt/spack/linux-fedora31-zen2/gcc-9.2.1/sz-2.1.8.3-nqdmiulwq47adbyuiukkkelbelshynyp
HDF5PATH = /home/dreistein/opt/spack/opt/spack/linux-fedora31-zen2/gcc-9.2.1/hdf5-1.10.6-tmlylf4wz64tgckx6tffr5z6vuw7s3wh

##=======================================================================
##   DIRECTORY TREE
##=======================================================================

LIB		= lib
OBJ		= obj
SRC		= src
INC		= include

##=======================================================================
##   COMPILERS
##=======================================================================

CC 		= gcc
MPICC 		= mpicc

##=======================================================================
##   FLAGS
##=======================================================================

SZFLAGS         = -I$(SZPATH)/include -L$(SZPATH)/lib

HDF5FLAGS	= -I$(HDF5PATH)/include #$(HDF5PATH)/lib/libhdf5.a

##=======================================================================
##   TARGETS
##=======================================================================

OBJS		= $(OBJ)/H5Z_SZ.o

SHARED		= libhdf5sz.so
STATIC		= libhdf5sz.a

all: 		$(LIB)/$(SHARED) $(LIB)/$(STATIC)

$(OBJ)/%.o:	$(SRC)/%.c
		@mkdir -p $(OBJ)
		$(CC) -c -fPIC -g -O3 -I./include $(HDF5FLAGS) $(SZFLAGS) $< -o $@
		
$(LIB)/$(SHARED):	$(OBJS)
		@mkdir -p $(LIB)
		$(CC) -O3 -shared -o $(LIB)/$(SHARED) $(OBJS) $(SZFLAGS) -lc -lSZ -lz -lzstd

$(LIB)/$(STATIC):	$(OBJS)
		@mkdir -p $(LIB)
		$(RM) $@
		$(AR) -cvq $@ $(OBJS)
		
install: $(LIB)/$(SHARED) $(LIB)/$(STATIC)
		install -d $(SZPATH)/lib  $(SZPATH)/include
		install $(INC)/* $(SZPATH)/include/
		install $(LIB)/* $(SZPATH)/lib/

uninstall:
		$(RM) $(SZPATH)/$(LIB)/libhdf5sz.* $(SZPATH)/$(INC)/H5Z_SZ.h

clean:
		rm -f $(OBJ)/*.o $(LIB)/*

.PHONY:		$(SHARED) $(STATIC) install uninstall clean


