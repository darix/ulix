OS=Linux
LD=ld
CC=gcc
OBJDUMP=objdump

ifeq ($(UNAME_S),Darwin)
  OS=MacOS
  LD=/usr/cross/bin/i586-elf-ld
  CC=/usr/cross/bin/i586-elf-gcc
  OBJDUMP=/usr/cross/bin/i586-elf-objdump
endif

CCOPTIONS=-nostdlib -std=gnu89 -ffreestanding -fforce-addr -fomit-frame-pointer -fno-function-cse -nostartfiles -m32 -mtune=i386 -momit-leaf-frame-pointer
# CCOPTIONS=-nostdlib -ffreestanding -mtune=i386 -momit-leaf-frame-pointer

# LDOPTIONS=-T process.ld -static -s --pie
LDOPTIONS=-Tprocess.ld -static -s --pie
# LDOPTIONS=-T process.ld -static -s

OBJECTS = $(patsubst %.c, %, $(wildcard *.c))

all: $(OBJECTS) copy

%: %.c
	$(CC) $(CCOPTIONS) -g $(LDOPTIONS) $^ ../ulixlib.o -o $@
	# $(CC) $(CCOPTIONS) -g $(LDOPTIONS) ../ulixlib.c $^ -o $@
	$(OBJDUMP) -M intel -D $@ > $@.dump

clean:
	rm $(OBJECTS)

copy:
	cp $(OBJECTS) ../diskfiles/bin/

# test: login.c
# 	/usr/cross/bin/i586-elf-objdump -M intel -D login > login.dump
