# RISC-V Instructions with 32-bit Binary Code

## 1. `beqz a5, 1017c`
- **Hex:** `0x02078863`
- **Binary:** `0000 0010 0000 0111 1000 1000 0110 0011`
- **Breakdown:**
  - Immediate: `0000 0010 000` (split for B-type)
  - RS1: `00111` (a5)
  - RS2: `00000`
  - Funct3: `000`
  - Opcode: `1100011`

---

## 2. `addi sp, sp, -16`
- **Hex:** `0xff010113`
- **Binary:** `1111 1111 0000 0001 0000 0001 0001 0011`
- **Breakdown:**
  - Immediate: `1111 1111 0000`
  - RS1: `00010` (sp)
  - Funct3: `000`
  - RD: `00010` (sp)
  - Opcode: `0010011`

---

## 3. `auipc a0, 0x12`
- **Hex:** `0x00012517`
- **Binary:** `0000 0000 0000 0001 0010 0101 0001 0111`
- **Breakdown:**
  - Immediate: `0000 0000 0001`
  - RD: `00010` (a0)
  - Opcode: `0010111`

---

## 4. `addi a0, a0, -340`
- **Hex:** `0xeac50513`
- **Binary:** `1110 1010 1100 0101 0000 0101 0001 0011`
- **Breakdown:**
  - Immediate: `1110 1010 1100`
  - RS1: `00010` (a0)
  - Funct3: `000`
  - RD: `00010` (a0)
  - Opcode: `0010011`

---

## 5. `sd ra, 8(sp)`
- **Hex:** `0x00113423`
- **Binary:** `0000 0000 0001 0001 0011 0100 0010 0011`
- **Breakdown:**
  - Immediate: `0000 0000 0001` (split for S-type)
  - RS1: `00010` (sp)
  - RS2: `00001` (ra)
  - Funct3: `010`
  - Opcode: `0100011`

---

## 6. `auipc ra, 0x0`
- **Hex:** `0x00000097`
- **Binary:** `0000 0000 0000 0000 0000 0000 1001 0111`
- **Breakdown:**
  - Immediate: `0000 0000 0000`
  - RD: `00001` (ra)
  - Opcode: `0010111`

---

## 7. `jalr zero`
- **Hex:** `0x000000e7`
- **Binary:** `0000 0000 0000 0000 0000 0000 1110 0111`
- **Breakdown:**
  - Immediate: `0000 0000 0000`
  - RS1: `00000` (zero)
  - Funct3: `000`
  - RD: `00000` (zero)
  - Opcode: `1100111`

---

## 8. `ld ra, 8(sp)`
- **Hex:** `0x00813083`
- **Binary:** `0000 1000 0001 0011 0000 1000 0011`
- **Breakdown:**
  - Immediate: `0000 1000`
  - RS1: `00010` (sp)
  - Funct3: `011`
  - RD: `00001` (ra)
  - Opcode: `0000011`

---

## 9. `li a5, 1`
- **Hex:** `0x00100793`
- **Binary:** `0000 0000 0001 0000 0000 0111 1001 0011`
- **Breakdown:**
  - Immediate: `0000 0000 0001`
  - RS1: `00000` (zero)
  - Funct3: `000`
  - RD: `00101` (a5)
  - Opcode: `0010011`

---

## 10. `sb a5, 1944(gp)`
- **Hex:** `0x78f18c23`
- **Binary:** `0111 1000 1111 0001 1000 1100 0010 0011`
- **Breakdown:**
  - Immediate: `0111 1000 1111` (split for S-type)
  - RS1: `00100` (gp)
  - RS2: `00101` (a5)
  - Funct3: `000`
  - Opcode: `0100011`

---

## 11. `addi sp, sp, 16`
- **Hex:** `0x01010113`
- **Binary:** `0000 0001 0000 0001 0000 0001 0001 0011`
- **Breakdown:**
  - Immediate: `0000 0001 0000`
  - RS1: `00010` (sp)
  - Funct3: `000`
  - RD: `00010` (sp)
  - Opcode: `0010011`

---

## 12. `ret`
- **Hex:** `0x00008067`
- **Binary:** `0000 0000 0000 0000 1000 0110 0111`
- **Breakdown:**
  - Immediate: `0000 0000 0000`
  - RS1: `00001` (ra)
  - Funct3: `000`
  - RD: `00000`
  - Opcode: `1100111`

---

## 13. `auipc a5, 0xffff0`
- **Hex:** `0xffff0797`
- **Binary:** `1111 1111 1111 1111 0000 0111 1001 0111`
- **Breakdown:**
  - Immediate: `1111 1111 1111`
  - RD: `00101` (a5)
  - Opcode: `0010111`

---

## 14. `addi a5, a5, -396`
- **Hex:** `0xe7478793`
- **Binary:** `1110 0111 0100 0111 1000 0111 1001 0011`
- **Breakdown:**
  - Immediate: `1110 0111 0100`
  - RS1: `00101` (a5)
  - Funct3: `000`
  - RD: `00101` (a5)
  - Opcode: `0010011`

---

## 15. `jr zero`
- **Hex:** `0x00078c63`
- **Binary:** `0000 0000 0000 0111 1000 1100 0110 0011`
- **Breakdown:**
  - Immediate: `0000 0000 0000` (split for JALR)
  - RS1: `00000` (zero)
  - Funct3: `000`
  - RD: `00000` (zero)
  - Opcode: `1100111`
