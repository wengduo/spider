TARGET=spider
SOURCES=$(wildcard *.cpp)
OBJS=$(patsubst %.cpp,%.o,$(SOURCES))

CXX:=g++
OPTIMIZATION?=-O2 -DNDEBUG
WARNINGS=-Wall -std=c++11
#WARNINGS=-Wall -Werror
REAL_CXXFLAGS=$(OPTIMIZATION) $(CXXFLAGS) $(WARNINGS) $(DEBUG) $(PROF) -lcrypt
REAL_LDFLAGS=$(LDFLAGS) $(PROF) -rdynamic -lpthread -levent -lcrypt -ldl



all: $(TARGET)
	@if [ ! -d ../download ]; then mkdir ../download; fi

$(TARGET): $(OBJS)
	$(CXX) -o $@ $(REAL_LDFLAGS) $^ -levent -lpthread -ldl

.cpp.o:
	$(CXX) -c $(REAL_CXXFLAGS) $< -levent -lpthread -ldl

clean:
	-rm -rf $(TARGET) $(OBJS)
	-rm -rf ../$(TARGET)

debug:
	$(MAKE) OPTIMIZATION="" DEBUG="-g -ggdb -g3"

gprof:
	$(MAKE) PROF="-pg" 

install:
	-cp -f $(TARGET) ../

.PHONY: all clean debug gprof install
