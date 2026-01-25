# 65C02MMU Verilog Core

The **65C02MMU** is a fully compatible **65C02 CPU core with an integrated MMU**, written in Verilog.
It extends the classic 8-bit 65C02 with transparent memory banking, protection, and multi-bank execution
— without introducing new opcodes or breaking existing software.

## Key Features

- **100% 65C02-compatible** instruction set (including Rockwell/WDC extensions)
- **Integrated MMU** using unused 6502/65C02 NOP opcodes (no new ISA required)
- **20-bit addressing (1 MiB)** supported today; wider modes planned
- **Two banking modes**
  - 4 KiB window banking (legacy-friendly)
  - Full 64 KiB banking (segmented execution)
- **Independent code and data banks** (JBANK vs FBANK)
- **Zero-cycle bank switching** for most operations
- **Bank-aware JMP/JSR/RTS/RTI** with automatic return-bank tracking
- **SRAM-backed JBANK stack** for deep cross-bank subroutine calls
- **Per-bank Zero Page & Stack relocation (ZBANK)**
- **Optional protected memory** using per-bank access keys
- **MMJ_STORAGE mode** for fast bank-to-bank memory copies
- **Minimal, transparent stalls** only when SRAM access is required
- **BANK_REG_MEM** option for direct MMU register access via memory map

## Design Goals

- Preserve the classic 65C02 programming model
- Avoid self-modifying code and I/O-based bank switching
- Enable large address spaces on small FPGA targets
- Support OS-like features such as tasks and memory isolation

## Status

- All standard 65C02 tests pass (including Klaus Dormann suite)
- Comprehensive MMU-specific testbenches included
- Suitable for FPGA SoCs, retro systems, and embedded designs

See the **65C02MMU Manual v1.3.1** for full documentation and examples.
