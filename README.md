﻿# recommendation-system
## Prepare for a dataset
- คอลัมน์ **ชื่อวิชา** ให้เปลี่ยนเป็น **course**
- คอลัมน์ **ชื่อนามสกุล** ให้เปลี่ยนเป็น **username**
- คอลัมน์ **อีเมล** ให้เปลี่ยนเป็น **email**
- คอลัมน์ **วุฒิการศึกษา** ให้เปลี่ยนเป็น **education**
- คอลัมน์ **อายุ** ให้เปลี่ยนเป็น **age**
- คอลัมน์ **เวลาที่ชำระเงิน** ให้เปลี่ยนเป็น **time**
- คอลัมน์ **สถานะการชำระเงิน** ให้เปลี่ยนเป็น **payment**
- คอลัมน์ **ที่อยู่** ให้เปลี่ยนเป็น **address**
## TF-IDF & Cosine Similarities
หาความคล้ายคลึ่งกันระหว่าง**คอร์ส**เรียนในคอลัมน์ **course**
## KNN
หาระดับความ**ชอบ**ของผู้เรียนแต่ละคนโดยพิจารณาจาก**ประวัติการเรียน** ได้แก่
- คอลัมน์ **email**: หากไม่กรอกอีเมล ให้ 0 คะแนน หากเป็นโดเมนอื่น ให้ 1 คะแนน หากโดเมนเป็น cmu ให้ 2 คะแนน
- คอลัมน์ **age**-**education**: ระยะห่างระหว่างอายุกับวุฒิการศึกษา
  - หากไม่เกิน 4 ปี (คาดว่ายังอยู่ในระบบการศึกษา) ให้ 0 คะแนน
  - หากอยู่ระหว่าง 4 ถึง 6 ปี (คาดว่าเพิ่งจบการศึกษา) ให้ 1 คะแนน
  - หากเกิน 6 ปี (คาดว่าไม่ได้อยู่ในระบบการศึกษา) ให้ 2 คะแนน
- คอลัมน์ **time**: หากไม่ได้ลงทะเบียนในเวลาที่เหมาะสม ให้ 0 คะแนน หากได้ลงทะเบียนในเวลาที่เหมาะสม ให้ 1 คะแนน (เวลาที่เหมาะสม 09:00 - 11:00 และ 15:00 - 16:00)
- คอลัมน์ **payment**: หากค้างชำระ ให้ 0 คะแนน หากไม่ผ่านการอนุมัติ ให้ 1 คะแนน หากชำระเงิน ให้ 2 คะแนน
- คอลัมน์ **address**: ไม่กรอกข้อมูลที่อยู่ ให้ 0 คะแนน หากกรอกข้อมูลที่อยู่ ให้ 1 คะแนน

```
คะแนน=1+(อีเมล*0.375)+(อายุ-วุฒิการศึกษา*0.25)+(เวลาที่สมัครอบรม*0.5)+(สถานะ*1)+(ที่อยู่*0.25)  # โดยที่ 1<=คะแนน<=5
```
