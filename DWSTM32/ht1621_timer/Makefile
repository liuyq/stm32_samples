
ARMGNU = arm-none-eabi
#ARMGNU = arm-linux-gnueabi

AOPS = --warn --fatal-warnings
COPS = -Wall -Werror -O2 -nostdlib -nostartfiles -ffreestanding

all : ht1621_timer.bin 

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

ht1621_timer.o : ht1621_timer.c
	$(ARMGNU)-gcc $(COPS) -mthumb -mcpu=cortex-m0 -march=armv6-m -c ht1621_timer.c -o ht1621_timer.o

ht1621_timer.bin : flash.ld flash.o ht1621_timer.o
	$(ARMGNU)-ld -o ht1621_timer.elf -T flash.ld flash.o ht1621_timer.o
	$(ARMGNU)-objdump -D ht1621_timer.elf > ht1621_timer.list
	$(ARMGNU)-objcopy ht1621_timer.elf ht1621_timer.bin -O binary

