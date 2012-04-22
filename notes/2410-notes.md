---
layout: default
---

�ҵ����� limingth@akaedu.org

Day1: section1: ���õ���
bootloader ��Ŀ����
1-LED		*
2-UART		*
3-stdio		#
4-printf	#
5-shell		#
6-command	#
7-loader	#
8-xmodem	*
9-clock		*
10-sdram	*
11-flash	*

C���Բ���
1��д�� main ����ԭ��
int main(int argc, char * argv[]);

2��д�� printf ����ԭ��
int printf(const char *, ...);

3��д��һ������ԭ�ͣ�������ֵ��ַ�����ת��
char * itoa(int num, char * buf);
char * gets(char * buf);

4��д��һ������ԭ�ͣ�����ַ��������ֵ�ת��
int atoi(const char *);

5��д��2������ԭ�ͣ�����ַ����Ŀ����ͱȽ�
char * strcpy(char * dst, const char * src);
int strcmp(const char * s1, const char * s2);

��Ŀ����
    �鳤	��Ա	 	
1�� ������	�º�	������
2�� ������	������	�ݸ���	��ҫ��
3�� ����	��ѩ�	����	�ƺ���	�����
4�� ������	����

1����Ա�������س�
Ӳ��֪ʶ��ARM�������˽⣬Ӣ����������֯�������

2��С���ѧϰĿ��
ϣ������Ŀ��ѧϰ����Щ֪ʶ��������Щ����

Day1: section2: Bootloader ��Ŀ����
һ����Ŀ����
bootloader ��Ŀ�ļ������� (www.zhaopin.com)
���⣺��δ��������ĸ���ҵ������
��ҵ����������ӡ��������ӡ�ҽ�Ƶ��ӡ�����
��ȫ���������ܼҾӡ��������񡢻����ˡ�������

������ĿĿ��
���⣺������ʵ��һ��bootloader����������Linux��
˼������Ŀ�Ŀ�������
1��׼������
�����Ĵ��Ӳ�� ���
Ӳ����akae2440/2410
�����ads 1.2

2����̱����ؼ�·����
1) Ӳ���Ǻõ�
2) �ܵ���ˣ��Լ�д�ĳ��� +LED, +GPIO
3) ������� +UART
4) �ܽ����� +SHELL
5) �������� +COMMAND
6) �������� +LOADER
------------------- ������bootloader
7) �ܵø����� +CLOCK
8) �ڴ������ +SDRAM
9) �ܱ���̻��� +FLASH
10) ���Լ����� +AUTORUN
------------------- �ӵ� bootloader -> app ������
11) ������linux�ں��ˣ������ں˴�ӡ����� +KERNEL
12) �ܼ��ظ��ļ�ϵͳ�����뵽 shell ��ʾ������ +ROOTFS
13) �ܹ�ͨ�����罻���� +NET
-------------------

Day1: section3: �����
���糩ͨ
�������� cmd, ping, ipconfig, path, 
c:\windows;c:\windows\system32
���ʹ���
\\192.168.0.24

tools �������
1) ADS1.2 �����׼� ��armcc �����У�
2) FoxitReader �Ķ��� ��ͼ�α�ע���ߣ�
3) Ultraedit �༭�� ������Ҽ�֧�֣�CTRL+h��

resource �������
оƬ�����ֲ�
�������Ӳ��ԭ��ͼ

Day1: section4: Ӳ�����
��Դ��H-jtag dection cpu: ARM920T
���ڣ�2�� 0x378(LPT), 0xDE00 (PCI-LPT)

NandFlash ����
0x00000000-0x00020000 : "vivi"
0x00020000-0x00030000 : "param"
0x00030000-0x001f0000 : "kernel"
0x00200000-0x04000000 : "root"

vivi (bootloader): 0x20000 = 128K 
1block = 32page = 512byte = 0.5K = 16K
128K = 16K * 8block

kernel (�ں�): 0x30000 = 192K = 12block
size = 0x1c0000 = 128K*14 = 112blocks => 124block

rootfs (�ļ�ϵͳ): 0x200000 = 128bock

MC2410E DEVELOP KIT

VIVI version 0.1.4 (root@Rhvd) (gcc version 2.95.2 20000516 (release) [Rebel.com]) #0.1.4 Thu May 4 00:58:37 CST 2006
MMU table base address = 0x33DFC000
Succeed memory mapping.
NAND device: Manufacture ID: 0xec, Chip ID: 0x76 (Samsung K9D1208V0M)
Found saved vivi parameters.
CS8900 - type: 630e, rev: a00
CS8900 - status: ad6 (EEPROM present)
Setting MAC address...
Display format changed to VGA 640X480 mode
Press Return to start the LINUX now, any other key for vivi
type "help" for help.
vivi> 
vivi> help

Day1: section5: ��������
ADS ��Ŀ �����ļ� .mcp (.prj)
AXD ���� ARMulator.dll ������� RDI (Remote Debug Interface)
ARM ��ִ���ļ� .axf (.exe .elf)

������п������������
���ڷ��ͼĴ�����ַ  0x50000020 
�޸� link ���� -ro-base 0x0
�޸� link ���� -entry __main (main -> __main)s


Day2: section1: ��������ԭ��
Ӳ�����ӹ�ϵ������ <--> S3c2410 cpu
רҵ���Ӳ��ԭ��ͼ (pdf)
����Ӳ������֪ʶ��
1) DB9 9��
2) ���� pin2(TxD), pin3(RxD), pin5(GND) ����
3) Max3232 ��ƽת��оƬ (TTL��ƽ(0-5v)->RS-232��ƽ(-15v->+15v
�ӵװ�ͺ��İ�ԭ��ͼ�鿴��֪ 
TxD -> K15/GPH2
RxD -> K17/GPH3
------------------------------------
רҵ���оƬ�����ֲ� (DataSheet)
S3C2410.pdf  
FBGA ��װ Pin Number/Pin Name
UART ���ڵ����Žӿ� - TxD/RxD nCTS/nRTS UEXTCLK
רҵ������Ź��ܸ��� (Selectable Pin Functions)
GPH2 (GPHCON) 0x56000070 
GPH2 [5:4] 	00 = Input     01 = Output
		10 = TXD0   11 = Reserved
------------------------------------

Day2: section2: ��������ԭ��2
SoC�ڲ������� (������ʲô�� ����Ҫ��10��)
ARM920T �ں�
	Processor Core, CP15, MMU, CACHE, AMBA BUS
BUS ���� 
	AHB BUS, APB BUS
Controllers ������
	CLOCK, Power, Mem controller, NandFlash, 
	Interrupt, Timer, DMA, UART, GPIO
	
0x1000 = 4K
0x100000 = 1M
1G = 0x40000000

UART ��������������ԭ��
רҵ������⹦�ܼĴ���SFR (Special Function Reg)	
��ַ��Χ  (0x48000000 - 0x5A000040)
		len = 0x12000000 = 256M
ռ�ô洢�� 4byte * 300 = 1K

���ڵ����⹦�ܼĴ���
���ƼĴ��� W
״̬�Ĵ��� R
���ݼĴ��� R/W

Day2: section3: ��������ԭ��3
���ڿ����� UART Controller �ı��
רҵ���ʱ��ͼ (Timing Diagram)
���ڵķ���ʱ��
1) ����״̬ '1'
2) ��ʼλ 1bit  1->0   (����16clock)
3) ����λ 8bits/7bits/6bits/5bits  (�鿴7,8,9clock)
4) У��λ none
5) ֹͣλ 1bit/1.5bit/2bits '1'	

UART Block Diagram (�ڲ��ṹ��ͼ)
��Ҫ��ɣ�Transmitter/Receiver (Buffer&Shifter), 
Control Unit, Baud Generator, Clock Source
DataBus, AddrBus, UEXTCLK 

UART SFRs
�Ĵ������


Day2: section4: ���ڼĴ�������
vivi> dump 0x50000000 0x40
50000000: 03 00 00 00 45 02 00 00-00 00 00 00 00 00 00 00 | ....E...........
50000010: 02 00 00 00 00 00 00 00-00 00 00 00 00 00 00 00 | ................
50000020: 00 00 00 00 0D 00 00 00-1A 00 00 00 00 00 00 00 | ................
50000030: 00 00 00 00 00 00 00 00-00 00 00 00 00 00 00 00 | ................

GPHCON: GPH4, GPH5 (Txd/Rxd)
ULCON: 	8bit(3)
UCON:	PCLK, polling mode 0101(5)
UBRDIV:	50M/(115200*16)-1 = 26 (0x1A)
UTXH:  	'h'

�ܽ᣺���������ؼ����� ����Ҫ������
1������������ŵĹ��ܸ���
2������λ 8bit	
3����żУ��λ none 
4��ֹͣλ 1bit
5�������� none
6�������� 115200
7������ʹ��/����ʹ��
8��ʱ��Դ PCLK (vivi 50Mhz)
9��������ʽ polling/interrupt  (DMA)

Day2: section5: �����������ʵ��
����Ҫ��ʵ��UART1����� "hello, world" (���޴�)

�κ���ҵ��
1��ʵ�ִ��ڵ���ؽӿ�,Ҫ�����淶,ѧ���ú��λ����(~,|,&)
void uart_init()
void uart_putchar(char c);
char uart_getchar(void);

2�����ڴ��ڵ� uart_put/getchar��������� stdio �ӿ�
int puts(char *);
char * gets(char *);

3����� printf ��ʽ����ӡ�����Ҫ��֧��%c,%s,%d,%x
printf("%c, %s, %d, %x\n", 'a', "hello", 100, 100);

day3: section 1: ��׼���ʵ��
#include <stdio.h>
/usr/include/stdio.h 	-Isubdir
ADS��װĿ¼����
putchar
	int putchar(int c);
getchar
	int getchar(void);
puts
	int puts(const char * s);
gets
	char *gets(char * s);
printf
	int printf(const char * format, ...);

�������֯�ṹ
main (#include "stdio.h")
-----
stdio (5 api) (#include "uart.h")
-----
uart (uart_xxx) (uart.c, uart.h)

�ַ� \r \n \b �ĺ���
\r (Enter) 	�س� ���ص����ף�
\n (Ctrl+Enter) ���� ������һ�У�
\b (BackSpace)	�˸� ������һ���ַ�������ɾ����
putchar('a');
putchar('\n');
putchar('b');
putchar('\n');
a
b

a
 b

puts("hello\n");
puts("world\n");
hello
world

hello
     world

printf("hello\n");

�����ն� (windows�Դ�) hypertrm.exe hypertrm.dll

ARM ��ϵ�ṹ�£�����ջ֡�ķ��䷽���ǣ�
1����ջ��ջ�Ŀռ��ǴӸߵ�ַ����͵�ַ���������ġ�
2����������ʽ���������Ƿ�����ջ�ϵģ���������ġ�
3��C�������ڱ���ʱ�����������ַ��˳�������Ĳ�������ջ��
4����һ�������ĵ�ַ���ͺ�̲����ĵ�ַ�Ĺ�ϵ�ǣ�p++

#if 1
	#include <stdarg.h>
#else
	typedef int *	va_list;
	#define va_start(p, fmt)	p = (va_list)&fmt + 1
	#define va_arg(p, type)		(type)(*p++);
	#define va_end(p)			p = (void *)0
#endif

����3�����1�����Ͷ���
���Ͷ����� typedef
va_start �꣺ͨ�� format �ĵ�ַ��ʹpָ���2�������ĵ�ַ
va_arg �꣺ͨ��p�õ���ǰ������ֵ����ʹpָ����һ������ ��ͨ�����ö�Σ�
va_end �꣺ʹpָ��� (0)

�κ���ҵ��
��� printf %d, %x ���������Ĵ�ӡ���
printf("a = %d, b = 0x%x %8x (%p)", 100, 0x64);
a = 100, b = 0x64 0x00000064

day4: section1: Shell ���������
md
md 0x0: SRAM �ڴ�
md 0x50000000: UART SFR
md 0x30000000: SDRAM �ڴ�

mw 0x0 0x11223344

help md

��ʽ md addr size
���� "   md     0x0  64  "
�����
0x00000000:  E52DE004 E24DD064 E28F2048 E3A01041 
0x00000010:  E28F0048 EB0000B5 E28F2038 E3A01041 
0x00000020:  E28F0038 EB0000B1 E3A03064 E3A02064 
0x00000030:  E3A01064 E28F0038 EB0000AC E28F0048 
����Ҫ��ʵ��һ�� shell_parse ����
int shell_parse(char * buf, char * argv[]);

int argc;
char * argv[5];
char buf[100];

argc = shell_parse(buf, argv);

day4: section2: md/mw ����ʵ��
bootloader $ md 0x11000300
�鿴 0x11000300 �ڴ��ַ
11000300: 00000000 00000009 31120000 00D300D3
11000310: 05480548 25580558 25580558 25580558
11000320: 05480548 25580558 25580558 25580558
11000330: 05480548 25580558 25580558 25580558

bootloader $ mw 0x1100030a 0x0 2
*(short *)0x1100030A = (short)0x0

bootloader $ md 0x11000300
�鿴 0x11000300 �ڴ��ַ
11000300: 00000000 00000009 30000000 630E630E
11000310: 05480548 25580558 25580558 25580558
11000320: 05480548 25580558 25580558 25580558
11000330: 05480548 25580558 25580558 25580558

bootloader $ mw 0x1100030a 0x20 2
review mem 0x1100030A:  0x30200000

bootloader $ md 0x11000300
11000300: 00000000 00000009 30200000 03000300
11000310: 05480548 25580558 25580558 25580558
11000320: 05480548 25580558 25580558 25580558
11000330: 05480548 25580558 25580558 25580558

day5: section1: Loader ʵ��
�µ����繲�� \\172.16.0.21
         UART
pc bin --------> board (SRAM/SDRAM)
        NET/USB

vivi> load ram 0xc00 88 x
Ready for downloading using xmodem...
Waiting...
(�˵������� -> �����ļ� -> 
test_uart0.bin -> 
xmodem Э�� -> ����
�ɹ�����ʾ
Downloaded file at 0x00000c00, size = 128 bytes
There are 0x0 bad blocks in this partition, please make it at least 0x28 bytes l
arger
vivi> go 0xc00
		
day5: section2: Xmodem Э��ʵ��
����
1. ���� size
2. ���ݰ� packet (0x1A���) 128 byte
3. ��ͷ + �����ݣ�+ ��β
    3       128      1 = 132
��Э�飺 �� 4 + bin datas
���͵Ĺ����У����ܻ�������
ʲô���⣿ 
1���������ӶϿ� ���ϵ�������
2���������ݵ�ͻ�� ����������ݣ�

Լ���� �շ�����
�����Ӧ�� ����
1��˭������ �������
2��˭��Ӧ�� ���Ӧ��

���ʵ�� my bootloader ����д����
1. ���� start.s ������ɲο� \\��ɽ-̫ԭ-ARM�γ�\codes\loader\start.s

2. �޸� DebugRel Setting, -> ARM Linker -> Layout -> start.o

3. main.c �ʼ ���һ�� �رտ��Ź� 
	// disable watch dog
	*(int *)0x53000000 = 0;
	
   uart.c ���棬PCLK �����ʼ������ 12M	
	// 12000000/19200/16 - 1 = 39.0 -1 = 38
	UBRDIV0 = 38;	
	
4. reset �����壬�� 19200 ���������� uart0 ����ͨѶ

�׶��ܽ᣺
һ��Ҫ�ܹ��Լ�������ɲ�����ʵ�ֵģ�
int add(int n, ...);
int printf(const char * format, ...);
���������ļ�����Ҫ����
stdio ���� gets ��ʵ�֣���Ҫ���� \r \n \b 
printf ���� va_list, va_start, va_arg, va_end
	ʵ�����º��� char * itoa(int a, char * buf)	
				void itoa_hex(int a, char * buf, int flag)
shell ����ʵ�ֵĺ���
	int shell_parse(char * buf, char * argv[])
	int strcmp(const char * s1, const char * s2)
	int atoi(char * buf)  10/16����
xmodem Э���ԭ���ʵ�� SOH, ACK, NAK, EOT, CAN
		�����Ĵ����� 1 + 2 + 128 + 1		

vivi> dump 0x48000000 64
48000000: 10 1D 11 22 00 07 00 00-00 07 00 00 7C 1F 00 00 | ..."........|...
48000010: 00 07 00 00 00 07 00 00-00 07 00 00 01 80 01 00 | ................
48000020: 01 80 01 00 E9 01 8E 00-B1 00 00 00 20 00 00 00 | ............ ...
48000030: 20 00 00 00 00 00 00 00-00 00 00 00 00 00 00 00 |  ...............
vivi> dump 0x4c000000 64
4C000000: FF FF FF 00 40 C0 05 00-32 80 04 00 F0 FF 0F 00 | ....@...2.......
4C000010: 04 00 00 00 03 00 00 00-00 00 00 00 00 00 00 00 | ................
4C000020: FF FF FF 00 40 C0 05 00-32 80 04 00 F0 FF 0F 00 | ....@...2.......
4C000030: 04 00 00 00 03 00 00 00-00 00 00 00 00 00 00 00 | ................
vivi> dump 0x4e000000 64
4E000000: 30 E8 00 00 00 00 00 00-00 00 00 00 A5 00 00 00 | 0........... ...
4E000010: 01 83 00 00 59 A9 95 00-00 00 00 00 00 00 00 00 | ....Y...........
4E000020: 00 00 00 00 00 00 00 00-00 00 00 00 00 00 00 00 | ................
4E000030: 00 00 00 00 00 00 00 00-00 00 00 00 00 00 00 00 | 
		
day6: section1: Clock ����
MPLL ���໷
	MPLLCON (PMS setting: PDIV/MDIV/SDIV)
	Fout = Fin * (MDIV+8) / (PDIV+2) / s^SDIV 
DIVN
	HDIVN: FCLK/HCLK
	PDIVN: HCLK/PCLK
	
day6: section2: Makefile ʹ��
���ߣ� armasm, armcc, armlink, fromelf
linux: (arm-linux-)as, gcc, ld, objdump/objcopy	
������ -c, -first, -ro-base, -bin, -c -d -s

day6: section3: SDRAM ����
volatile �ؼ��� - ��ֹ�Ż���ǿ�Ʒô�
JTAG��Joint Test Action Group ����(����)����дrom������ram
SRAM/SDRAM/NandFlash/NorFlash �������ϵ

SRAM
6���������ɴ�����
	����С���۸���ٶȿ죬���綪ʧ������ˢ��
SDRAM
1������ܺ�1�����ݣ��������ݵĳ�ŵ�����������
	�����󣬼۸���ˣ��ٶ��������綪ʧ����Ҫˢ��

�ӽӿڵ�·�Ϻ�����������
SRAM: ��ַ�ߣ������ߣ������ߣ�Ƭѡ�ź�
2*8bit SRAM: ������ƴ��16λ����ַ�߶���A0

SDRAM ������Ҫ��
�����ص㣺��̬ˢ�£�����ѡͨ������ƴ�գ��ڲ���BANK
��������ʵ�֣�
���ŵĹ��ܸ��� ��û�и��ã��������ã�
����������
1���������ߵĿ�� 32bit -> A2 <-> A0
2��������SDRAM���е�ַ���9bit
3��RAS to CAS delay ��ѡͨ����ѡͨ����ʱ����
4��SDRAM����������64M -> ��ַ����26��
5��SDRAM������ˢ������ 7.8us -> 8196 cycles/64 ms

day7: section1: Flash ����
NandFlash �����ص�
�޵�ַ�ߣ���ַ�ź���ͨ�������ߴ��ݵģ�Ҳ���ǵ�ַ�����ݸ���
������Ҳֻ��8����ÿ��ֻ�ܴ���1��byte
64M ����Ҫ26����ַ�źţ�ÿ�δ�8bit������Ҫ��4��
ÿ�γ���������ֻ��8bit

���豸��ÿ�ζ����Զ�1��pages
�����Է�Ϊ�ϰ�ҳ(����00) �°�ҳ(����01)

����Ҳ��ͨ�� IO0-IO7 �����ݸ�NandFlash
�����źŵĸ��ã������ַ������

SDRAM������
4 banks * 2^13 * 2^9 * 4bytes = 2^26 = 64M

NandFlash�ڲ�����ɽṹ
4096 blocks * 32 pages * (512+16)bytes = 64M 

NorFlash �����ص�
�е�ַ�ߣ����Ҳ��ø��ã���һ�ε�ַ���ܹ���������
��SRAM�Ķ�ȡ��ʽһ�������Կ��������������������ִ��
���ۣ�NorFlash����ֱ������bootloader������SRAM����
SROM = SRAM + ROM(NorFlash) bank0-bank5
oneNand -> new NorFlash = [SRAM Interface + (NandFlash)]

4pin usb interface + NandFlash

������ҵҪ��
1��ͨ�� read ID ��ʱ��ͼ��������ؼĴ���������оƬID
	0xEC 0x76 0x?? 0x??

2��ͨ�� read page ��ʱ��ͼ��������0��ַ��ʼ��512�ֽ�
���� md �������ʽ��ӡ ���򻯰취��0�ֽں�511�ֽڣ�
�����ӡ buf[0] buf[511];

3��ʵ�� mybootloader ��������ʵ�� autorun ����
��������ǰ�� test-uart.bin �� Hjtag ��д�� Flash
autorun ����ʱ��ͨ�� nand_read �ӿڶ�ȡ�� sdram
go �� sdram ȥִ�С� ����û������ˣ�����뵽 shell

1M = 16K * 64 blocks

�ܹ�ʵ��һ�� nr (nandread) �����ʽ
nr nand_addr sdram_addr size

chapter 2, 3 (Arch, Ins)
14 (Int)   8 (DMA)

day8: section1: ARM ��ϵ�ṹ����
�쳣���� ϵͳ���� printf ������ʵ��
SoC оƬ�ڲ��Ľṹ���ں�+������(Watchdog,GPIO,UART,CLOCK,SDRAM,NandFlash) 
ARM�ں˵Ľṹ��ARM920T (ProcessorCore,CP15,MMU,CACHE,AMBA bus)
Processor Core: 
�Ƽ��Ķ����� ARM �� X86 ����ʷ (�������룬intel)

��Ҫ����
1) Processor Operating State ����������״̬
ARM ״̬��32bit ָ��
THUMB ״̬: 16bit ָ�� -> BX ins

2) processor mode ������ģʽ
���쳣
�� User (usr): The normal ARM program execution state
�� System (sys): A privileged user mode for the operating system
�쳣
�� IRQ (irq): Used for general-purpose interrupt handling
�� FIQ (fiq): Designed to support a data transfer or channel process
�� Supervisor (svc): Protected mode for the operating system
�� Abort mode (abt): Entered after a data or instruction prefetch abort
�� Undefined (und): Entered when an undefined instruction is executed

3) Big/Little-Endian format ��β��/Сβ��
(int *)0 => 0x12345678

 78   56   34   12
---- ---- ---- ----
  0    1    2    3
  
*(short *)1 = ?	 0x3456

4) Register �Ĵ�����֯
37 �� = 31 ͨ��(r0-r15) + 6 ״̬(CPSR,SPSR)
31 = 16 + 7 + 2 + 2 + 2 + 2
31 = 8*1(r0-r7) + 5*2(r8-r12) + 2*6(r13,r14) + 1*1(r15-pc)

6 = 1*1(CPSR) + 1*5(SPSR)

5) Exception �쳣
Exception arise �쳣�¼����� ���쳣������
0x0:  	1. ��λ�쳣 -> SVCģʽ
0x4:	2. ִ��δ����ָ�� -> UNDģʽ
0x8:	3. ִ������ж�ָ��(SWI) -> SVCģʽ ��ϵͳ���ã�
0xc:	4. PrefetchԤȡָ����ֹ -> ABTģʽ
0x10:	5. PrefetchԤȡ������ֹ -> ABTģʽ
0x18:	6. IRQ ��ͨ�ж� -> IRQģʽ
0x1c:	7. FIQ �����ж� -> FIQģʽ

Exception Priority (Prio) �쳣�������ȼ�
1. ��λ
2. ������ֹ
3. �����ж�
4. ��ͨ�ж�
5. ָ����ֹ

6. δ����ָ��/����ж�ָ���쳣

�쳣����/��������/�˳���
* �쳣����/�쳣��Ӧ ��Ӳ����ɣ�
1�����淵���ϵ�ַ (PC+4) �� LR_irq
2�����淵����ģʽ (CPSR) �� SPSR_irq
3���޸�CPSR�������µ�ģʽ IRQ
4���޸�PC����ת���µĵ�ַ-�쳣������ 0x8/0x18
���������
5�������ֳ� r0-r12 -> stack
	stmfd r13!, {r0-r12}
	
* �쳣����/�쳣�ָ� �������ɣ�
0��������ָ��ֳ� r0-r12 <- stack
	ldmfd r13!, {r0-r12}
1��LR -> PC �ָ���ַ
2��SPSR -> CPSR �ָ�ģʽ
	movs pc, lr
	
3������ж����λ

day8: section2: ARM ָ�
0xE 3A 0DD40 
���������immediate 
D40 = 0x1000 : 0001 0000 0000 0000
B40 = 0x10000: 0001 0000 0000 0000 0000
940 = 0x100000
740	= 0x1000000
xYY: 
x-�����ݣ���λ�ĸ���
YY-��Ч���� 0x40 : 0b0100 0000
��Ч����:û����λ֮ǰ����
x: ѭ������2*xλ 26λ�� ����6λ


SWI ����ж�ָ�����ת�� 0x8 ��ַ

mov pc, lr ��ַ����
0xe1a0f00e
�����ķ��أ� ģʽҲ����
movs pc, lr
0xe1b0f00e

0xe0803001	 add r3, r0, r1
0xe0823003	 add r3, r2, r3
0xe1b0f00e	 movs pc, r14

0x10 + X*4 = 0x802c (handler)	
0xEA002007	b handler

0x10 + ? * 4 = 0x8018

0xEA002002

day9: section1: system call ϵͳ���õ�ʵ��
boot> md 0x30008000
boot> mw 0x30008000 0xEF000005
	swi 0x5 -> 0xef000005
boot> md 0x30008000
boot> go 0x30008000

0x30008004
b   .		[0xeafffffe]

���˼·��
1. �����쳣������ʵ��2�� b
2. swi_handler: �����ֳ� {r0-r12, lr}
3. ά�ֱ��� r0 �������mov r0, #0x68	bl uart_putchar
4. �ָ��ֳ�
5. �����쳣������

day9: section2: Interrupt �жϴ���
�жϵ�3�����ģ��

            nIRQ
ARM920T <---------- Interrupt CONT <------ INT-SOURCES: GPIO
								   <------ UART, USB, SD 

0xFE, 0xFD, 0xBF
0xBC <----> 1011 1100

Pending (suspend) ����δ����
SRCPND

	���� GPF0 Ϊ EINT ��ʽ��ѡ���ù��ܣ�
bootloader $ mw 0x56000050 0x2

	���� EINT0 Ϊ Falling Edge Trigger ���½��ش�����
bootloader $ mw 0x56000088 0x2

	�鿴 SRCPND �Ĵ���
bootloader $ md 0x4a000000
4A000000: 02000000 00000000 FFFFFFFF 0000007F
4A000010: 00000000 00000000 00000003 0000FFFF
	��ʱ���� Key3 ����������һ���жϣ��ٴβ鿴 SRCPND
4A000000: 02000001 00000000 FFFFFFFF 0000007F
4A000010: 00000000 00000000 00000003 0000FFFF
	�����μĴ��� 0 λ INTMSK
bootloader $ mw 0x4a000008 0xFFFFFFFE
	�ٴβ鿴 SRCPND, INTPND
buf = <md>
4A000000: 02000001 00000000 00000000 000000FF
4A000010: 00000001 00000000 00000003 0000FFFF
	��θ� Pending λ����� д1��0
	�������� SRCPND ������� INTPND���� OK
	�������� INTPND ������� SRCPND�������ã������ٱ��Զ�����1
	
��Ϊ�жϵĹؼ����룺 bootloader ���޸�
1����Ϊ�û�ģʽ�����޸� CPSR������bootloader��ֱ�Ӵ��ж� 
0xD0 -> 0x50

2��irq_handler ����Ҫ���2��PND�Ĵ��������� clear_int

3����󷵻��� subs pc, lr, #4	������ movs pc, lr

�ж� Timer ��ʱ���ж�chp10�� DMA �ж�chp8

�ܽ᣺
1�������������� �쳣���ж� vs �жϴ�����쳣����
                 ARM Core		Board (SoC)

���ж�IRQ���쳣
				 
2������жϴ����ȫ���̣�����һ��
A. �жϵĳ�ʼ����Ϊ�жϵķ����������� -> ����ģ��
a1) �ж�Դ�ĳ�ʼ����GPIO, UART, Timer, DMA��
	1. �ж�Դ��ʹ�ܣ������ж�Դ���жϵķ�ʽ������֪ͨ�ϼ�(INT CONT.)
	2. �жϵĴ�����ʽ�������ж�Դ�жϴ�������
a2) �жϿ������ĳ�ʼ�����Ա����ϼ��㱨 (ARM920T)
	0. �ж� pending λȫ�����һ��
	1. �жϵ�����λ��
	2. �жϵ����ȼ�����
a3) ARM���ں��ж��쳣λ��ʹ��
	1. CPSR I-bit/F-bit

B. �жϵ���Ӧ�ʹ����Լ�����
�ж������߱����жϷ����ˣ����һ������Ӳ�����У��жϣ��쳣��Ӧ
b1) (�ж�)�쳣��Ӧ��Ӳ���Զ����
	1. �����ַ�� PC->LR_irq
	2. ����ģʽ�� CPSR->SPSR_irq
	3. �޸�ģʽ:  IRQ_mode -> CPSR (0xD2)
	4. �޸ĵ�ַ:  0x18 -> PC ��ʱ��������ת��ͬʱģʽ����л�
b2) (�ж�)�쳣��������ֹ�ʵ��
	0. ͵����������������һ�� sp_irq: mov sp, #0x33000000
	1. �ֳ��ı��棺STMFD sp!, {r0-r12, lr}
	2. �쳣�������: ע���������C����lr_irq��Ҫ����
	3. �ֳ��Ļָ�: LDMFD sp!, {r0-r12, lr}
	4. �쳣�ķ���: movs pc, lr	(ģʽ�͵�ַͬʱ����)
b3) �жϵ����⴦��
	0. �ж�ģʽ�µ� SP ջָ��ĳ�ʼ��
	1. �ж�pendingλ�����
		SRCPND -> INTPND �Ⱥ����⣬Ҫն���ȳ���
	2. �ж��쳣���ص�ʱ����Ҫ subs pc, lr, #4	
	 
day10: section1: Timer ��ʱ���жϴ���	
Timer ��
1��Clock ����
����ʱ��
��Ƶ
�����Ĵ��� counter--
PWM �ź������ռ�ձ�

50M = 50000000  -->  <65535 = 50000
50000000 -> 100000 -> 1/2 -> 50000
-------- =  200000 -> 1/4 -> 50000
250

ʱ�Ӻͷ�Ƶ
TCFG0��250 - 1 = 249 (8-bit prescaler)
TCFG1��1/4 ��Ƶ

������ 
TCNTB0�� = 50000
TCON�� set Manual update bit
TCON�� set Start bit
TCON�� clear Manual update bit

day11��section1��Ƕ��ʽLinux����
1��Ӳ������
*Communication
RS232(DB9), Ethernet (RJ45), 
PS/2, USB(Host/Device),

*Multimedia
LCD+Ts(40pin), VGA, TV
Audio output/in(MIC), 

*Storage
SD, IDE, 

*Interface
Key, Jtag, 

2����ҪоƬ
S3C2410(cpu), HY57V561620C(SDRAM), 
k9f1208(NandFlash), sst39vf160(NorFlash)
CS8900/DM9000(Net), UDA1341/WM9714(Audio)

day11��section2�����濪�������
su �л�������Աģʽ������Ϊ 123456
rpm -ivh --force *.rpm
vi /etc/profile
���ϵͳ��ִ���ļ�·��
export PATH=$PATH:/opt/host/armv4l/bin:/sbin

armv4l-unknown-linux-gcc hello.c -o hello

4������绷�� - �Դ�
startx ����ͼ��ϵͳ
ifconfig ���Լ�ip
ping �Լ�ip
ping 192.168.0.1

route add default gw 192.168.0.1
ping 8.8.8.8  ����pingͨ����
ping www.baidu.com ����������
�����ͨ������� /etc/resolv.conf  ����������
nameserver 8.8.8.8
nameserver 210.73.64.1
nameserver 202.106.0.20

�ܷ� ping ��ͨ��һ���ؼ�����
iptables -F �ر�Linux�ķ���ǽ
windows XP ��֮���Ƶ��� �������->����Internet����->windows����ǽ->�ر�(���Ƽ�)

ftp server (ftpd:21)
���� server�� /etc/init.d/vsftpd restart/stop/start
ftp 172.16.0.101
> username : akaedu
passwd: akaedu
> ls
> get
> put
> bye/quit
�����ļ��� /etc/vsftpd/vsftpd.conf
��Ŀ¼�� /home/akaedu/

webserver (httpd:80)
���� server: /etc/init.d/httpd restart/stop/start
http://172.16.0.101
���Կ�������ҳ test page
�����ļ��� /etc/httpd/conf/httpd.conf
��Ŀ¼�� /var/www/html/

day11��section3��Ƕ��ʽLinux�ں˱���
tar zxvf linux-br.tar.gz ��ѹ
du [-sh] �鿴Ŀ¼�ļ���С
find . -name *.c | wc �鿴���� c �ļ� (4000+ ��c����)

vmlinux: ��ʵ���� linux ���ںˣ����� ELF ��ʽ���ں�
zImage���������������д�������ϵģ�û�и�ʽ��bin�ļ��ں�
       ld
*.o ------> vmlinux

	objcopy
vmlinux-----> zImage

make menuconfig 
	General Setup
	Char Device - ����
	Block Device
	MTD Device - NandFlash
	Network Device - Cs8900
make dep
make vmlinux
make zImage

zImage �� arch/arm/boot Ŀ¼��, ������ /home/akaedu
cp arch/arm/boot/zImage /home/akaedu

�л��� D: �� ftp ���أ��޸�binary����ģʽ��get zImage

�� zImage ��д����12block�� �� 0x30000 ��
1M: 12block 12*16K = 192K ��

�� mycramfs.img ��д����128block�� �� 0x200000 ��
1M: 128block 128*16K = 2M ��

�� vivi ��д�� 0block

C:\Documents and Settings\Administrator>type my.cmd
akaedu
akaedu
binary
get zImage
bye

C:\Documents and Settings\Administrator>ftp -s:my.cmd 172.16.0.101
Connected to 172.16.0.101.
220 (vsFTPd 1.1.3)
User (172.16.0.101:(none)):
331 Please specify the password.

230 Login successful. Have fun.
ftp> dir
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        0            4096 Jan 19 18:17 arm
drwx------    4 500      500          4096 Apr 28 17:23 evolution
drwxr-xr-x    2 500      500          4096 Apr 28 14:36 hello
-rw-r--r--    1 0        0            5143 Apr 28 15:30 hello.1
drwxr-xr-x    2 0        0            4096 Mar 23 15:53 image
drwxr-xr-x    2 0        0            4096 Apr 28 15:41 led
-rw-r--r--    1 500      500           755 Apr 28 15:25 led.c
drwxrwxr-x    3 500      500          4096 Apr 28 15:41 lwj
drwxrwxr-x    4 500      500          4096 Apr 28 16:58 mc2410
drwxr-xr-x    2 0        0            4096 Jan 19 18:19 skyeye
-rwxrwxr-x    1 500      500        989788 Apr 28 19:05 zImage
226 Directory send OK.
ftp: �յ� 696 �ֽڣ���ʱ 0.01Seconds 46.40Kbytes/sec.
ftp> get zImage
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for zImage (989788 bytes).
226 File send OK.
ftp: �յ� 989788 �ֽڣ���ʱ 0.03Seconds 31928.65Kbytes/sec.
ftp> bye
221 Goodbye.

��ȡflash���� zImage �ŵ� 0x30008000 ����Ȼ�� go
nr 0x30000 0x30008000 0x100000

Source Insight ��Դ��

�õ�һ�� rootfs ��img�ļ���
mkcramfs root_china my-cramfs.img
ftp ������������д�� 128block

./mnt/etc/init.d/rcS
#exec /usr/etc/rc.local

/var/www/html/hello
wget http://172.16.0.101/hello

	
	




	
				 













								   



