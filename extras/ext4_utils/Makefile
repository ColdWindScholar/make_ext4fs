SELIB = ../../libselinux
ZLLIB = ../../zlib/src
COLIB = ../../core
SPLIB = ../../core/libsparse
OBJS = ext4fixup.o ext4_utils.o allocate.o contents.o extent.o \
	indirect.o uuid.o sha1.o wipe.o crc16.o ext4_sb.o canned_fs_config.o
MKE4FS_OBJS = make_ext4fs_main.o make_ext4fs.o
EXT4FIX_OBJS = ext4fixup_main.o ext4fixup.o

ifeq ($E,.exe)
OBJS += windows_supp.o regex/regex.o
endif

all: make_ext4fs$E ext4fixup$E

make_ext4fs$E: $(MKE4FS_OBJS) $(OBJS) $(SELIB)/src/libselinux.a $(SPLIB)/libsparse.a $(ZLLIB)/libz.a
	$(LD) $(LDFLAGS) -o $@ $^ $(LIBS)

ext4fixup$E: $(EXT4FIX_OBJS) $(OBJS) $(SELIB)/src/libselinux.a $(SPLIB)/libsparse.a $(ZLLIB)/libz.a
	$(LD) $(LDFLAGS) -o $@ $^ $(LIBS)

%.o: %.c
	$(CC) $(CFLAGS) -I. -I$(SELIB)/include -I$(SPLIB)/include -I$(COLIB)/include -o $@ $<

clean:
	rm -f $(MKE4FS_OBJS) $(OBJS)
	rm -f make_ext4fs$E
