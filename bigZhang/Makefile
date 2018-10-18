vpath %.S conf
vpath %.c conf/Src Hal_Driver/Src Hal_Driver/Src/Legacy
vpath %.h conf/Inc Hal_Driver/Inc Hal_Driver/Inc/Legacy CMSIS/Include

DEFS += -DUSE_HAL_DRIVER -DSTM32F429xx
PATHSSRC += Hal_Driver/Src
PATHSINC += Hal_Driver/Inc
INCS += -Iconf/Inc -IHal_Driver/Inc -IHal_Driver/Inc/Legacy -ICMSIS/Include

OBJS += conf/startup_stm32f429xx.o conf/Src/system_stm32f4xx.o 
OBJS += conf/Src/stm32f4xx_it.o conf/Src/stm32f429i_discovery.o
OBJS += $(PATHSSRC)/stm32f4xx_hal_i2c_ex.o $(PATHSSRC)/stm32f4xx_hal_spi.o 
OBJS += $(PATHSSRC)/stm32f4xx_hal_flash.o $(PATHSSRC)/stm32f4xx_hal_rcc_ex.o  
OBJS += $(PATHSSRC)/stm32f4xx_hal_dma.o $(PATHSSRC)/stm32f4xx_hal_pwr.o  
OBJS += $(PATHSSRC)/stm32f4xx_hal.o $(PATHSSRC)/stm32f4xx_hal_flash_ex.o  
OBJS += $(PATHSSRC)/stm32f4xx_hal_gpio.o $(PATHSSRC)/stm32f4xx_hal_cortex.o 
OBJS += $(PATHSSRC)/stm32f4xx_hal_rcc.o $(PATHSSRC)/stm32f4xx_hal_i2c.o 
OBJS += $(PATHSSRC)/stm32f4xx_hal_pwr_ex.o  
    
OBJS += main.o

CFLAGS += -mcpu=cortex-m4 -mthumb -Wall 
LFLAGS += -mcpu=cortex-m4 -mthumb 

all:blink.bin
clean:
	@rm -f $(OBJS) blink.bin blink.elf
	
blink.bin:blink.elf
	@arm-none-eabi-objcopy -O binary -S $< $@
	
blink.elf:$(OBJS)
	@arm-none-eabi-gcc $(LFLAGS) $^ -Tconf/STM32F429ZITx_FLASH.ld -o $@
	@arm-none-eabi-size $@
	
burn:blink.bin
	@st-flash write $< 0x08000000
	
%.o:%.S
	@arm-none-eabi-gcc $(CFLAGS) -c $< -o $@
%.o:%.c
	@arm-none-eabi-gcc $(CFLAGS) $(DEFS) $(INCS) -c $< -o $@
