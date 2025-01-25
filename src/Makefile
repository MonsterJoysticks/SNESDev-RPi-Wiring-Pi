CC=gcc
SRCDIR=.
BUILDDIR=../build
CFLAGS=-Wall -O3
LIBS=-lwiringPi -lpthread -lrt -lconfuse 

TARGET := SNESDev
SRCEXT := c
SOURCES := $(shell find $(SRCDIR) -type f -name "*.$(SRCEXT)")
OBJECTS := $(patsubst $(SRCDIR)/%,$(BUILDDIR)/%,$(SOURCES:.$(SRCEXT)=.o))
DEPS := $(OBJECTS:.o=.deps)

all $(TARGET):$(OBJECTS)
	@echo " Linking..."; $(CC) $^ $(LIBS) -o $(TARGET)

$(BUILDDIR)/%.o: $(SRCDIR)/%.$(SRCEXT)
	@mkdir -p $(BUILDDIR)
	@echo " CC $<"; $(CC) $(CFLAGS) -MD -MF $(@:.o=.deps) -c -o $@ $<


check:
	# TO BE DONE! JUST A DUMMY FOR NOW
	@echo "*** NO TESTS IMPLEMENTED ***"

clean:
	@echo " Cleaning..."; $(RM) -r $(BUILDDIR) $(TARGET)
	@echo " Cleaning WiringPi..."; $(RM) -r $(BUILDDIR) $(TARGET)
-include $(DEPS)

install:
	install -d $(DESTDIR)$(bindir)
	install -m 0755 $(TARGET) $(DESTDIR)$(bindir)
	install -m 0755 ../supplementary/snesdev.cfg $(DESTDIR)/$(sysconfdir)

uninstall:
	-rm $(DESTDIR)$(bindir)/$(TARGET)
	-rm $(DESTDIR)/$(sysconfdir)/snesdev.cfg

.PHONY: clean install uninstall
