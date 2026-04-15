# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** luannguyenaivietnam@gmail.com
**Name:** Nguyen Le Minh Luan
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Ket qua chinh xac, Laptop la san pham electronics dat nhat sau khi da loai bo du lieu khong hop le |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Ket qua sai hoan toan do du lieu chua Extreme Outlier, Duplicate ID, NULL values va wrong data type |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung garbage_data.csv, Agent dua ra ket qua hoan toan sai vi nhieu van de chat luong du lieu nghiem trong:

**Duplicate IDs:** File garbage co hai record voi id=1 (Laptop va Banana). Dieu nay gay nham lan khi truy van du lieu, lam mat di tinh nhat quan cua dataset. Agent khong the biet ban ghi nao la chinh xac.

**Wrong Data Types:** Record "Broken Chair" co price = "ten dollars" thay vi so. Neu Agent co tinh toan so hoc, se gap loi ngay lap tuc. Trong truong hop nay, pandas co the co xu huong khac nhau khi xu ly kieu du lieu sai.

**Extreme Outlier:** San pham "Nuclear Reactor" co gia $999,999, lon bat thuong so voi cac san pham con lai. Vi Agent dung logic tim san pham gia cao nhat trong category electronics, no chon Nuclear Reactor thay vi Laptop. Day la vi du dien hinh cua outlier lam lech hoat dong cua AI Agent.

**Null Values:** Record "Ghost Item" co id=None va category=None. Khi Agent loc theo category, cac NULL values nay co the gay ra loi hoac cho ket qua khong mong doi.

**Ket luan phan tich:** Garbage data khong chi cho ket qua sai ma con co the pha vo toan bo logic cua Agent. Trong moi truong san xuat, du lieu chat luong kem la nguyen nhan chinh dan den AI Agent hoat dong khong dang tin cay.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y hoan toan.

Du cho prompt co duoc viet ky cang den dau, neu du lieu dau vao (knowledge base) cua Agent bi nhiem doc boi garbage data thi ket qua tra ve van se sai. Trong bai thi nghiem nay, Agent dung logic rat don gian nhung van cho ket qua chinh xac khi dung clean data, va cho ket qua hoan toan sai khi dung garbage data. Dieu nay chung minh rang: "Garbage In, Garbage Out" - chat luong du lieu quyet dinh chat luong dau ra cua AI. ETL pipeline voi validation chat che la nen tang bat buoc cho bat ky he thong AI nao.
