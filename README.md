Thinpad SRAM adapter
========

https://qurisc-docs.readthedocs.io/zh_CN/latest/sections/peripheral.html#sram

Usage
--------

It is recommended that you put the tri-state at the top module.

```
wire[19:0] sram_addr;
wire sram_ce;
wire[63:0] sram_data;
wire sram_oe;
wire sram_we;

wire[63:0] sram_din;
wire[63:0] sram_dout;
wire sram_bidir;
assign ext_ram_data=sram_bidir?sram_dout[63:32]:32'bZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ;
assign base_ram_data=sram_bidir?sram_dout[31:0]:32'bZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ;

assign sram_din={ext_ram_data, base_ram_data};
assign base_ram_addr=sram_addr;
assign ext_ram_addr=sram_addr;
assign base_ram_ce_n=sram_ce;
assign base_ram_oe_n=sram_oe;
assign base_ram_we_n=sram_we;
assign ext_ram_ce_n=sram_ce;
assign ext_ram_oe_n=sram_oe;
assign ext_ram_we_n=sram_we;

some_module yourmodule(
    .din_0(sram_din),
    .dout_0(sram_dout),
    .sram_addr_0(sram_addr),
    .sram_be_0({ext_ram_be_n, base_ram_be_n}),
    .sram_ce_0(sram_ce),
    .sram_oe_0(sram_oe),
    .sram_we_0(sram_we)
);

```
