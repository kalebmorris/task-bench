MPICXX ?= mpicxx

DEBUG ?= 0

CXXFLAGS ?=
CXXFLAGS += -std=c++11 -I../core

LDFLAGS ?=
# FIXME: Would prefer static linking, but some MPI implementations don't support it.
LDFLAGS += -L../core -lcore_s

ifeq ($(strip $(DEBUG)),0)
	CXXFLAGS += -O3
else
	CXXFLAGS += -O0 -ggdb
endif

include ../core/make_blas.mk

all: nonblock basic bcast alltoall buffered_send

alltoall: alltoallv.cc
	$(MPICXX) -o $@ $(CXXFLAGS) $< $(LDFLAGS)

basic: basic.cc
	$(MPICXX) -o $@ $(CXXFLAGS) $< $(LDFLAGS)

bcast: bcast.cc
	$(MPICXX) -o $@ $(CXXFLAGS) $< $(LDFLAGS)

buffered_send: buffered_send.cc
	$(MPICXX) -o $@ $(CXXFLAGS) $< $(LDFLAGS)

nonblock: nonblocking.cc
	$(MPICXX) -o $@ $(CXXFLAGS) $< $(LDFLAGS)

clean:
	rm -f *.o
	rm -f alltoall
	rm -f basic
	rm -f bcast
	rm -f buffered_send
	rm -f nonblock
