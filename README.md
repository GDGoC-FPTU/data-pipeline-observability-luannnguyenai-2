[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574233&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** luannguyenaivietnam@gmail.com
**Name:** Nguyen Le Minh Luan

---

## Mo ta

Bai lab nay xay dung mot ETL pipeline hoan chinh gom 4 buoc: Extract du lieu tu JSON, Validate loai bo record khong hop le (price <= 0 hoac category rong), Transform chuan hoa du lieu (Title Case + tinh discounted_price giam 10%) va Load ket qua ra file CSV co timestamp. Ngoai ra, bai lab thuc hien thi nghiem Stress Test de quan sat tac dong cua du lieu kem chat luong den ket qua cua AI Agent.

- **Tong so record tho:** 5
- **Record hop le (processed):** 3 (Laptop, Chair, Monitor)
- **Record bi loai (dropped):** 2 (Mystery Box gia -10, Phone khong co category)
- **Discounted price:** giam 10% so voi gia goc

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

Ket qua: tao ra file `processed_data.csv` voi cac records da duoc validate va transform.

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao du lieu sach (chay solution.py truoc)
python solution.py

# Buoc 2: Tao du lieu rac
python generate_garbage.py

# Buoc 3: So sanh ket qua Agent
python agent_simulation.py
```

### Chay Tests (Autograder)
```bash
pytest tests/test_autograder.py -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (extract, validate, transform, load)
├── agent_simulation.py      # RAG-like Agent simulation
├── generate_garbage.py      # Script tao garbage data de Stress Test
├── raw_data.json            # Du lieu dau vao (5 records)
├── processed_data.csv       # Output cua ETL pipeline (3 records sach)
├── garbage_data.csv         # Du lieu rac de test Agent
├── experiment_report.md     # Bao cao thi nghiem Stress Test
└── README.md                # File nay
```

---

## Ket qua

| Buoc | Chi tiet |
|------|----------|
| Extract | Doc 5 records tu raw_data.json |
| Validate | Giu lai 3 records hop le, loai 2 records loi (gia <= 0 va category rong) |
| Transform | Category chuyen thanh Title Case, them discounted_price = price * 0.9, them cot processed_at |
| Load | Luu 3 records ra processed_data.csv |

**Stress Test:**
- Clean Data: Agent cho ket qua chinh xac - "Laptop at $1200"
- Garbage Data: Agent cho ket qua sai - "Nuclear Reactor at $999999" (do Extreme Outlier)
