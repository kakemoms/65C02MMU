# 65C02MMU Verilog Core

The **65C02MMU** is a fully compatible **65C02 CPU core with an integrated MMU** OR ***a stand-alone MMU that can operate beside a real 6502/65C02***, all written in Verilog. 
They extends the classic 8-bit 65C02 with transparent memory banking, protection, and multi-bank execution
— without introducing new opcodes or breaking existing software.

Three versions:
**cpu_65c02_v1.3.7z** - A full 65C02 core with the 65MMU integrated into the core (old 20-bit version).
**cpu_65c02_v1.4.7z** - A full 65C02 core with the 65MMU integrated into the core (24-bit version).
**65MMU.7z** - The 65MMU that can be used stand-alone beside a real 65C02. Also contains a wrapper to compile it together with (any) 6502/65C02 verilog core.

## Key Features

- **100% 65C02-compatible** instruction set (including Rockwell/WDC extensions)
- **Integrated MMU** using unused 6502/65C02 NOP opcodes (no new ISA required)
- **20-bit or 24-bit addressing (1 MiB or 16 MiB)** supported today (V1.3: 20-bit or V1.4: 24-bit)
- **Two banking modes**
  - 4 KiB window banking (legacy-friendly, but only for integrated MMU)
  - Full 64 KiB banking (segmented execution - all MMU verions)
- **Independent code and data banks** (JBANK vs FBANK)
- **Zero-cycle bank switching** for most operations
- **Bank-aware JMP/JSR/RTS/RTI** with automatic return-bank tracking
- **SRAM-backed JBANK stack** for deep cross-bank subroutine calls
- **Per-bank Zero Page & Stack relocation (ZBANK)**
- **Optional protected memory** using per-bank access keys
- **MMJ_STORAGE mode** for fast bank-to-bank memory copies
- **Minimal, transparent stalls** only when SRAM access is required
- **BANK_REG_MEM** option for direct MMU register access via memory map
- **Full Test Suite** for testing all aspects of the 65C02 and the new MMU
  
## Design Goals

- Preserve the classic 65C02 programming model
- Avoid self-modifying code and I/O-based bank switching
- Enable large address spaces on small FPGA targets
- Support OS-like features such as tasks and memory isolation

## Status

- All standard 65C02 tests pass (including Klaus Dormann suite)
- Comprehensive MMU-specific testbenches included
- Suitable for FPGA SoCs, retro systems, and embedded designs

See the **65C02MMU Manual v1.3.1 or v1.4** for full documentation and examples.

## Known bugs
Version 1.3:
- Setting BANK_REG_MEM bit ON, displays the internal registers in the $0000-$01FF area. Registers in the $0200-$03FF area are not shown.
- Writing to the internal registers in the $0000-$01FF area does not work properly and can lead to a cpu crash.
- Old DIHOLD logic (problem with the RDY signal)
Version 1.4:
- No known bugs (all V.1.3 bugs fixed)

## License
This project is licensed under the GNU GPL v3.0.
(C) Renato Bugge 2026
