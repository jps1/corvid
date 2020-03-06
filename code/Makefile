### make changes accordingly ###
CC       = gcc
CPP      = g++
CLINKER  = gcc
CCLINKER = g++
MAKE     = make --no-print-directory
SHELL    = /bin/sh
CFLAGS		= -Wall -pedantic -DDSFMT_MEXP=19937 -msse2 -DHAVE_SSE2 
OPTI            = -O3 -march=native
#OPTI = -pg # for profiling
LDFLAGS	= -lm
INCLUDES	= 
LIBS	= 
OBJS	= corvid.o epimodel.o params.o epimodelparameters.o dSFMT19937.o bnldev.o
DEFINES = -DVERBOSE

default: corvid

corvid: $(OBJS) Makefile
	$(CCLINKER) -o corvid $(OBJS) $(OPTI) $(LDFLAGS) $(LIBS) $(DEFINES)

R0corvid: $(OBJS) Makefile R0model.o R0model.h
	$(CCLINKER) -o R0corvid R0model.o epimodel.o params.o epimodelparameters.o dSFMT19937.o bnldev.o $(LDFLAGS) $(LIBS) $(DEFINES)

%.o: %.cpp epimodel.h epimodelparameters.h params.h Makefile
	$(CPP) $(CFLAGS) $(OPTI) $(INCLUDES) $(DEFINES) -c $<

dSFMT19937.o: dSFMT.c dSFMT.h dSFMT-params19937.h Makefile
	$(CC) $(CFLAGS) $(OPTI)  -std=c99 --param max-inline-insns-single=1800 -fno-strict-aliasing -Wmissing-prototypes -msse2 -DHAVE_SSE2 -DNDEBUG $(INCLUDES) $(DEFINES) -c dSFMT.c -o dSFMT19937.o

bnldev.o: bnldev.c bnldev.h Makefile
	$(CC) $(CFLAGS) $(OPTI) $(INCLUDES) $(DEFINES) -c bnldev.c -o bnldev.o

zip: *.c *.cpp *.h Makefile README LICENSE HISTORY examples/*
	cd ..; zip corvid/corvid.zip corvid/README corvid/LICENSE corvid/gpl.txt corvid/HISTORY corvid/Makefile corvid/*.cpp corvid/*.c corvid/*.h corvid/one-*dat corvid/seattle-*dat corvid/la-*dat corvid/usa-*dat corvid/examples/*

emacs:
	emacs Makefile *.R *.h *.c *.cpp README HISTORY &

clean:
	rm -f *.o corvid R0corvid *~
	rm -f Summary? Tracts? Log? Individuals?
	echo 0 > run-number