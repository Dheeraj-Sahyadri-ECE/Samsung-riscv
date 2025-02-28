# Samsung-riscv
Repository for Samsung RISC-V Talent Development Program

The program harnesses the RISC-V architecture and employs open-source tools to instruct individuals on the design of VLSI chips and the fundamentals of RISC-V

BASIC DETAILS:

Name: Dheeraj

College: Sahyadri college of Engineering and management,Adyar,Mangalore-575007

College mail: dheeraj.ec23@sahyadri.edu.in

Email ID: dheerajdheeru794@gmail.com

GitHub profile:https://github.com/Dheeraj-Sahyadri-ECE

Linkedin profile:https://www.linkedin.com/in/dheeraj-57b2a932a


Task1
![Task1 2](https://github.com/user-attachments/assets/5729e9de-58cc-4941-9c31-15f6302ffb39)
![Task1](https://github.com/user-attachments/assets/e290a5ab-57b4-452a-9827-330abce11987)
![Task1 1](https://github.com/user-attachments/assets/8670711e-5690-47c6-9992-6a503a0bc8b3)
Task2
![task2](https://github.com/user-attachments/assets/e8f27413-0a29-4361-8ac8-8f0f8ee7928e)
![task2 1](https://github.com/user-attachments/assets/8fc79c92-794a-410d-8334-8e9c0fe25e78)
Task3

Task 3.1
![IMG-20250217-WA0000](https://github.com/user-attachments/assets/8237dd2d-93cc-47c0-882b-429bc3596bf2)
Task 3.2
![image](https://github.com/user-attachments/assets/ee46fb9d-542d-4942-ba19-105bc91616da)

### **RISC-V Instruction Types and Fields**  

RISC-V instructions are categorized into different types based on how their fields are structured. These fields include:  
- **Opcode (7 bits)**: Identifies the type of instruction.  
- **funct3 (3 bits)**: Specifies the operation within the instruction type.  
- **funct7 (7 bits, only for R-type)**: Further refines the operation.  
- **Register Fields (rd, rs1, rs2)**: Specify the registers involved.  
- **Immediate (various sizes)**: Represents constants used in operations.  

Each instruction type is designed for specific operations.  

---

## **1. R-type (Register Type)**  
### **Used for:** Arithmetic and logical operations involving registers.  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| funct7    | 7       | Defines the operation (e.g., addition vs. subtraction). |
| rs2       | 5       | Second source register. |
| rs1       | 5       | First source register. |
| funct3    | 3       | Additional operation information. |
| rd        | 5       | Destination register. |
| opcode    | 7       | Instruction category. |

### **Example:** `add a0, a1, a2`  
- Adds `a1` and `a2`, storing the result in `a0`.  
- **Binary Encoding:**  
  ```
  funct7   | rs2  | rs1  | funct3 | rd   | opcode  
  0000000  | 00110 | 00101 | 000   | 00100 | 0110011  
  ```
---

## **2. I-type (Immediate Type)**  
### **Used for:** Immediate operations, loads, and jumps.  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| imm[11:0] | 12      | Signed immediate value. |
| rs1       | 5       | Source register. |
| funct3    | 3       | Operation type. |
| rd        | 5       | Destination register. |
| opcode    | 7       | Instruction category. |

### **Example:** `addi a0, a1, 10`  
- Adds `10` to `a1`, storing the result in `a0`.  
- **Binary Encoding:**  
  ```
  imm[11:0] | rs1  | funct3 | rd   | opcode  
  000000001010 | 00001 | 000   | 00010 | 0010011  
  ```
---

## **3. S-type (Store Type)**  
### **Used for:** Storing values into memory.  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| imm[11:5] | 7       | Upper part of immediate value. |
| rs2       | 5       | Data register. |
| rs1       | 5       | Base address register. |
| funct3    | 3       | Operation type. |
| imm[4:0]  | 5       | Lower part of immediate value. |
| opcode    | 7       | Instruction category. |

### **Example:** `sw a0, 16(sp)`  
- Stores `a0` at memory address `sp + 16`.  
- **Binary Encoding:**  
  ```
  imm[11:5] | rs2  | rs1  | funct3 | imm[4:0] | opcode  
  0000010   | 00010 | 00010 | 010   | 00000    | 0100011  
  ```
---

## **4. B-type (Branch Type)**  
### **Used for:** Conditional branching (e.g., `beq`, `bne`).  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| imm[12|10:5] | 7  | Split upper immediate part. |
| rs2       | 5       | Second register for comparison. |
| rs1       | 5       | First register for comparison. |
| funct3    | 3       | Defines branch type (e.g., equal, not equal). |
| imm[4:1|11] | 5  | Split lower immediate part. |
| opcode    | 7       | Instruction category. |

### **Example:** `beq a0, a1, 16`  
- If `a0 == a1`, jump to `PC + 16`.  
- **Binary Encoding:**  
  ```
  imm[12|10:5] | rs2  | rs1  | funct3 | imm[4:1|11] | opcode  
  000000 | 00001 | 00000 | 000   | 00000 | 1100011  
  ```
---

## **5. U-type (Upper Immediate Type)**  
### **Used for:** Loading large immediate values (`lui`, `auipc`).  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| imm[31:12] | 20      | Immediate value (upper bits). |
| rd        | 5       | Destination register. |
| opcode    | 7       | Instruction category. |

### **Example:** `lui a0, 0x12345`  
- Loads `0x12345000` into `a0`.  
- **Binary Encoding:**  
  ```
  imm[31:12] | rd   | opcode  
  00010010001101000101 | 00010 | 0110111  
  ```
---

## **6. J-type (Jump Type)**  
### **Used for:** Jumping to an address (`jal`).  

### **Fields:**
| **Field**  | **Bits** | **Description** |
|-----------|---------|----------------|
| imm[20|10:1|11|19:12] | 20  | Immediate value for target address (split). |
| rd        | 5       | Destination register (stores return address). |
| opcode    | 7       | Instruction category. |

### **Example:** `jal ra, 1024`  
- Jumps to address `PC + 1024` and stores return address in `ra`.  
- **Binary Encoding:**  
  ```
  imm[20|10:1|11|19:12] | rd   | opcode  
  000000100000 | 00001 | 1101111  
  ```
---

## **Summary of Instruction Types**
| **Type** | **Purpose** | **Example** |
|----------|------------|-------------|
| **R-type** | Register operations | `add a0, a1, a2` |
| **I-type** | Immediate operations, loads | `addi a0, a1, 10` |
| **S-type** | Store operations | `sw a0, 16(sp)` |
| **B-type** | Conditional branching | `beq a0, a1, 16` |
| **U-type** | Large immediate values | `lui a0, 0x12345` |
| **J-type** | Unconditional jumps | `jal ra, 1024` |

Each type is designed for a specific set of operations, making RISC-V simple yet powerful.  
Task 4

Task 4.1
![image](https://github.com/user-attachments/assets/b91dda78-084d-4b2e-9852-ae84f8eb11c3)
Task 4.2
![image](https://github.com/user-attachments/assets/8491a6d5-d95a-48ae-8496-395a17f2c503)
Task 4.3
![image](https://github.com/user-attachments/assets/79f7006f-c339-46da-a76b-2f27d798377a)
Task 4.4
![image](https://github.com/user-attachments/assets/4dabce91-918a-4fc8-8e38-4acc3cef9faf)
Task 4.5
![image](https://github.com/user-attachments/assets/6267f3ee-3573-48aa-9fee-fa4be09fd943)


Task 5

Automatic Light System using VSDSquadron Mini RISC-V Board, an IR sensor, and an LED for motion-based lighting control. The IR sensor detects movement, triggering the LED to blink three times before staying ON. If no motion is detected, the LED turns ON. This system is ideal for home automation, security, offering smart, hands- free lighting control.
![canva](https://github.com/user-attachments/assets/96a4abf3-0aac-4a32-880a-421be0fc8649)

code

#include <ch32v00x.h>
#include <debug.h>

void GPIO_Config(void)
{
    GPIO_InitTypeDef GPIO_InitStructure = {0};
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
    
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOD, &GPIO_InitStructure);
    
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOD, &GPIO_InitStructure);
}

int main(void)
{
    uint8_t IR = 0;
    uint8_t set = 1;
    uint8_t reset = 0;
    uint8_t a = 0;
    
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_Config();
    
    while (1)
    {
        IR = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_4);
        if (IR == 1)
        {
            for (a = 0; a < 3; a++)
            {
                GPIO_WriteBit(GPIOD, GPIO_Pin_6, set);
                Delay_Ms(200);
                GPIO_WriteBit(GPIOD, GPIO_Pin_6, reset);
                Delay_Ms(100);
            }
        }
    }
}


Task 6


Automatic Light System using VSDSquadron Mini RISC-V Board, an IR sensor, and an LED for motion-based lighting control. The IR sensor detects movement, triggering the LED to blink three times before staying ON. If no motion is detected, the LED turns ON. This system is ideal for home automation, security, offering smart, hands- free lighting control.

https://drive.google.com/file/d/1XeyxHFDsJVCskxtsd1dUFd7X-Bw9_cwQ/view?usp=drivesdk
