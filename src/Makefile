
# Intel Compiler
#CFLAGS = -O2  -I/opt/SPOOLES/2.2/ -DARCH="Linux" -DSPOOLES -DARPACK -DMATRIXSTORAGE -DNETWORKOUT -DUSE_MT
CFLAGS = -O2  -I/opt/SPOOLES/2.2/ -DARCH="Linux" -DSPOOLES -DARPACK -DMATRIXSTORAGE -DNETWORKOUT
FFLAGS = -O2
# GNU compiler
##CFLAGS = -Wall -O2  -I/opt/SPOOLES/2.2/ -DARCH="Linux" -DSPOOLES -DARPACK -DMATRIXSTORAGE -DNETWORKOUT -DUSE_MT
#CFLAGS = -Wall -O2  -I/opt/SPOOLES/2.2/ -DARCH="Linux" -DSPOOLES -DARPACK -DMATRIXSTORAGE -DNETWORKOUT
#FFLAGS = -Wall -O2

# Intel Compiler
CC=mpiicc
FC=mpiifort
# GNU compiler
#CC=cc
#FC=gfortran

.c.o :
	$(CC) $(CFLAGS) -c $<
.f.o :
	$(FC) $(FFLAGS) -c $<

include Makefile.inc

SCCXMAIN = ccx_2.20.c

OCCXF = $(SCCXF:.f=.o)
OCCXC = $(SCCXC:.c=.o)
OCCXMAIN = $(SCCXMAIN:.c=.o)

DIR=/opt/SPOOLES/2.2

#LIBS = $(DIR)/spooles.a -larpack -llapack -lblas -lpthread -lm -lc
LIBS = $(DIR)/spooles.a -larpack -llapack -lblas -lpthread -lm -lc

## Intel Compiler
ccx_2.20: $(OCCXMAIN) ccx_2.20.a
	./date.pl; $(CC) $(CFLAGS) -c ccx_2.20.c; $(FC)  -O2 -nofor-main  -o $@ $(OCCXMAIN) ccx_2.20.a $(LIBS) -qopenmp

ccx_2.20.a: $(OCCXF) $(OCCXC)
	ar vr $@ $?
