# Repair initiative covers eligible costs above an agreed deductible

The officer has an approved eligible supplier cost, a known exclusion, reimbursement already credited to that cost and remaining award ceiling. Reimbursement is 1 of (cost less excluded amount less deductible 25, floored at zero), rounded half up; there is no independent per-cost cap. Only the still-eligible portion can be claimed up to remaining award. A passed claim under this reimbursement policy debits grant receivable and credits grant income if earning and claim approval coincide. Recovery is a review amount on a prior claim, awaiting the authorized credit/repayment decision.

Read the input columns left to right. All amounts are in the stated book currency, at two decimal places unless a column identifies foreign units or a rate. Each row is an independent transaction or cutoff. Apply the stated local policy before comparing your result.

| Case | Original cost | Excluded cost | Already claimed | Award left before | Earned cumul. | New claim Dr/Cr | Review recovery | Earned over ceiling | Award left after | Decision |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FC-EXCESS-INSURANCE-001 | 31.25 | 0.00 | 0 | 12.50 | 6.25 | 6.25 | 0.00 | 0.00 | 6.25 | approve |
| FC-EXCESS-INSURANCE-002 | 31.25 | 0.00 | 0 | 65 | 6.25 | 6.25 | 0.00 | 0.00 | 58.75 | approve |
| FC-EXCESS-INSURANCE-003 | 31.25 | 0.00 | 0 | 150 | 6.25 | 6.25 | 0.00 | 0.00 | 143.75 | approve |
| FC-EXCESS-INSURANCE-004 | 31.25 | 0.00 | 0 | 350 | 6.25 | 6.25 | 0.00 | 0.00 | 343.75 | approve |
| FC-EXCESS-INSURANCE-005 | 31.25 | 0.00 | 3.13 | 12.50 | 6.25 | 3.12 | 0.00 | 0.00 | 9.38 | approve |
| FC-EXCESS-INSURANCE-006 | 31.25 | 0.00 | 3.13 | 65 | 6.25 | 3.12 | 0.00 | 0.00 | 61.88 | approve |
| FC-EXCESS-INSURANCE-007 | 31.25 | 0.00 | 3.13 | 150 | 6.25 | 3.12 | 0.00 | 0.00 | 146.88 | approve |
| FC-EXCESS-INSURANCE-008 | 31.25 | 0.00 | 3.13 | 350 | 6.25 | 3.12 | 0.00 | 0.00 | 346.88 | approve |
| FC-EXCESS-INSURANCE-009 | 31.25 | 0.00 | 14.06 | 12.50 | 6.25 | 0.00 | 7.81 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-010 | 31.25 | 0.00 | 14.06 | 65 | 6.25 | 0.00 | 7.81 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-011 | 31.25 | 0.00 | 14.06 | 150 | 6.25 | 0.00 | 7.81 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-012 | 31.25 | 0.00 | 14.06 | 350 | 6.25 | 0.00 | 7.81 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-013 | 31.25 | 0.00 | 25.00 | 12.50 | 6.25 | 0.00 | 18.75 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-014 | 31.25 | 0.00 | 25.00 | 65 | 6.25 | 0.00 | 18.75 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-015 | 31.25 | 0.00 | 25.00 | 150 | 6.25 | 0.00 | 18.75 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-016 | 31.25 | 0.00 | 25.00 | 350 | 6.25 | 0.00 | 18.75 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-017 | 31.25 | 3.91 | 0 | 12.50 | 2.34 | 2.34 | 0.00 | 0.00 | 10.16 | approve |
| FC-EXCESS-INSURANCE-018 | 31.25 | 3.91 | 0 | 65 | 2.34 | 2.34 | 0.00 | 0.00 | 62.66 | approve |
| FC-EXCESS-INSURANCE-019 | 31.25 | 3.91 | 0 | 150 | 2.34 | 2.34 | 0.00 | 0.00 | 147.66 | approve |
| FC-EXCESS-INSURANCE-020 | 31.25 | 3.91 | 0 | 350 | 2.34 | 2.34 | 0.00 | 0.00 | 347.66 | approve |
| FC-EXCESS-INSURANCE-021 | 31.25 | 3.91 | 3.13 | 12.50 | 2.34 | 0.00 | 0.79 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-022 | 31.25 | 3.91 | 3.13 | 65 | 2.34 | 0.00 | 0.79 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-023 | 31.25 | 3.91 | 3.13 | 150 | 2.34 | 0.00 | 0.79 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-024 | 31.25 | 3.91 | 3.13 | 350 | 2.34 | 0.00 | 0.79 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-025 | 31.25 | 3.91 | 14.06 | 12.50 | 2.34 | 0.00 | 11.72 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-026 | 31.25 | 3.91 | 14.06 | 65 | 2.34 | 0.00 | 11.72 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-027 | 31.25 | 3.91 | 14.06 | 150 | 2.34 | 0.00 | 11.72 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-028 | 31.25 | 3.91 | 14.06 | 350 | 2.34 | 0.00 | 11.72 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-029 | 31.25 | 3.91 | 25.00 | 12.50 | 2.34 | 0.00 | 22.66 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-030 | 31.25 | 3.91 | 25.00 | 65 | 2.34 | 0.00 | 22.66 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-031 | 31.25 | 3.91 | 25.00 | 150 | 2.34 | 0.00 | 22.66 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-032 | 31.25 | 3.91 | 25.00 | 350 | 2.34 | 0.00 | 22.66 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-033 | 31.25 | 10.31 | 0 | 12.50 | 0.00 | 0.00 | 0.00 | 0.00 | 12.50 | no eligible remainder |
| FC-EXCESS-INSURANCE-034 | 31.25 | 10.31 | 0 | 65 | 0.00 | 0.00 | 0.00 | 0.00 | 65.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-035 | 31.25 | 10.31 | 0 | 150 | 0.00 | 0.00 | 0.00 | 0.00 | 150.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-036 | 31.25 | 10.31 | 0 | 350 | 0.00 | 0.00 | 0.00 | 0.00 | 350.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-037 | 31.25 | 10.31 | 3.13 | 12.50 | 0.00 | 0.00 | 3.13 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-038 | 31.25 | 10.31 | 3.13 | 65 | 0.00 | 0.00 | 3.13 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-039 | 31.25 | 10.31 | 3.13 | 150 | 0.00 | 0.00 | 3.13 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-040 | 31.25 | 10.31 | 3.13 | 350 | 0.00 | 0.00 | 3.13 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-041 | 31.25 | 10.31 | 14.06 | 12.50 | 0.00 | 0.00 | 14.06 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-042 | 31.25 | 10.31 | 14.06 | 65 | 0.00 | 0.00 | 14.06 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-043 | 31.25 | 10.31 | 14.06 | 150 | 0.00 | 0.00 | 14.06 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-044 | 31.25 | 10.31 | 14.06 | 350 | 0.00 | 0.00 | 14.06 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-045 | 31.25 | 10.31 | 25.00 | 12.50 | 0.00 | 0.00 | 25.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-046 | 31.25 | 10.31 | 25.00 | 65 | 0.00 | 0.00 | 25.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-047 | 31.25 | 10.31 | 25.00 | 150 | 0.00 | 0.00 | 25.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-048 | 31.25 | 10.31 | 25.00 | 350 | 0.00 | 0.00 | 25.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-049 | 31.25 | 23.44 | 0 | 12.50 | 0.00 | 0.00 | 0.00 | 0.00 | 12.50 | no eligible remainder |
| FC-EXCESS-INSURANCE-050 | 31.25 | 23.44 | 0 | 65 | 0.00 | 0.00 | 0.00 | 0.00 | 65.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-051 | 31.25 | 23.44 | 0 | 150 | 0.00 | 0.00 | 0.00 | 0.00 | 150.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-052 | 31.25 | 23.44 | 0 | 350 | 0.00 | 0.00 | 0.00 | 0.00 | 350.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-053 | 31.25 | 23.44 | 3.13 | 12.50 | 0.00 | 0.00 | 3.13 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-054 | 31.25 | 23.44 | 3.13 | 65 | 0.00 | 0.00 | 3.13 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-055 | 31.25 | 23.44 | 3.13 | 150 | 0.00 | 0.00 | 3.13 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-056 | 31.25 | 23.44 | 3.13 | 350 | 0.00 | 0.00 | 3.13 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-057 | 31.25 | 23.44 | 14.06 | 12.50 | 0.00 | 0.00 | 14.06 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-058 | 31.25 | 23.44 | 14.06 | 65 | 0.00 | 0.00 | 14.06 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-059 | 31.25 | 23.44 | 14.06 | 150 | 0.00 | 0.00 | 14.06 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-060 | 31.25 | 23.44 | 14.06 | 350 | 0.00 | 0.00 | 14.06 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-061 | 31.25 | 23.44 | 25.00 | 12.50 | 0.00 | 0.00 | 25.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-062 | 31.25 | 23.44 | 25.00 | 65 | 0.00 | 0.00 | 25.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-063 | 31.25 | 23.44 | 25.00 | 150 | 0.00 | 0.00 | 25.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-064 | 31.25 | 23.44 | 25.00 | 350 | 0.00 | 0.00 | 25.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-065 | 79.99 | 0.00 | 0 | 12.50 | 54.99 | 12.50 | 0.00 | 42.49 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-066 | 79.99 | 0.00 | 0 | 65 | 54.99 | 54.99 | 0.00 | 0.00 | 10.01 | approve |
| FC-EXCESS-INSURANCE-067 | 79.99 | 0.00 | 0 | 150 | 54.99 | 54.99 | 0.00 | 0.00 | 95.01 | approve |
| FC-EXCESS-INSURANCE-068 | 79.99 | 0.00 | 0 | 350 | 54.99 | 54.99 | 0.00 | 0.00 | 295.01 | approve |
| FC-EXCESS-INSURANCE-069 | 79.99 | 0.00 | 8.00 | 12.50 | 54.99 | 12.50 | 0.00 | 34.49 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-070 | 79.99 | 0.00 | 8.00 | 65 | 54.99 | 46.99 | 0.00 | 0.00 | 18.01 | approve |
| FC-EXCESS-INSURANCE-071 | 79.99 | 0.00 | 8.00 | 150 | 54.99 | 46.99 | 0.00 | 0.00 | 103.01 | approve |
| FC-EXCESS-INSURANCE-072 | 79.99 | 0.00 | 8.00 | 350 | 54.99 | 46.99 | 0.00 | 0.00 | 303.01 | approve |
| FC-EXCESS-INSURANCE-073 | 79.99 | 0.00 | 36.00 | 12.50 | 54.99 | 12.50 | 0.00 | 6.49 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-074 | 79.99 | 0.00 | 36.00 | 65 | 54.99 | 18.99 | 0.00 | 0.00 | 46.01 | approve |
| FC-EXCESS-INSURANCE-075 | 79.99 | 0.00 | 36.00 | 150 | 54.99 | 18.99 | 0.00 | 0.00 | 131.01 | approve |
| FC-EXCESS-INSURANCE-076 | 79.99 | 0.00 | 36.00 | 350 | 54.99 | 18.99 | 0.00 | 0.00 | 331.01 | approve |
| FC-EXCESS-INSURANCE-077 | 79.99 | 0.00 | 63.99 | 12.50 | 54.99 | 0.00 | 9.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-078 | 79.99 | 0.00 | 63.99 | 65 | 54.99 | 0.00 | 9.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-079 | 79.99 | 0.00 | 63.99 | 150 | 54.99 | 0.00 | 9.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-080 | 79.99 | 0.00 | 63.99 | 350 | 54.99 | 0.00 | 9.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-081 | 79.99 | 10.00 | 0 | 12.50 | 44.99 | 12.50 | 0.00 | 32.49 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-082 | 79.99 | 10.00 | 0 | 65 | 44.99 | 44.99 | 0.00 | 0.00 | 20.01 | approve |
| FC-EXCESS-INSURANCE-083 | 79.99 | 10.00 | 0 | 150 | 44.99 | 44.99 | 0.00 | 0.00 | 105.01 | approve |
| FC-EXCESS-INSURANCE-084 | 79.99 | 10.00 | 0 | 350 | 44.99 | 44.99 | 0.00 | 0.00 | 305.01 | approve |
| FC-EXCESS-INSURANCE-085 | 79.99 | 10.00 | 8.00 | 12.50 | 44.99 | 12.50 | 0.00 | 24.49 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-086 | 79.99 | 10.00 | 8.00 | 65 | 44.99 | 36.99 | 0.00 | 0.00 | 28.01 | approve |
| FC-EXCESS-INSURANCE-087 | 79.99 | 10.00 | 8.00 | 150 | 44.99 | 36.99 | 0.00 | 0.00 | 113.01 | approve |
| FC-EXCESS-INSURANCE-088 | 79.99 | 10.00 | 8.00 | 350 | 44.99 | 36.99 | 0.00 | 0.00 | 313.01 | approve |
| FC-EXCESS-INSURANCE-089 | 79.99 | 10.00 | 36.00 | 12.50 | 44.99 | 8.99 | 0.00 | 0.00 | 3.51 | approve |
| FC-EXCESS-INSURANCE-090 | 79.99 | 10.00 | 36.00 | 65 | 44.99 | 8.99 | 0.00 | 0.00 | 56.01 | approve |
| FC-EXCESS-INSURANCE-091 | 79.99 | 10.00 | 36.00 | 150 | 44.99 | 8.99 | 0.00 | 0.00 | 141.01 | approve |
| FC-EXCESS-INSURANCE-092 | 79.99 | 10.00 | 36.00 | 350 | 44.99 | 8.99 | 0.00 | 0.00 | 341.01 | approve |
| FC-EXCESS-INSURANCE-093 | 79.99 | 10.00 | 63.99 | 12.50 | 44.99 | 0.00 | 19.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-094 | 79.99 | 10.00 | 63.99 | 65 | 44.99 | 0.00 | 19.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-095 | 79.99 | 10.00 | 63.99 | 150 | 44.99 | 0.00 | 19.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-096 | 79.99 | 10.00 | 63.99 | 350 | 44.99 | 0.00 | 19.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-097 | 79.99 | 26.40 | 0 | 12.50 | 28.59 | 12.50 | 0.00 | 16.09 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-098 | 79.99 | 26.40 | 0 | 65 | 28.59 | 28.59 | 0.00 | 0.00 | 36.41 | approve |
| FC-EXCESS-INSURANCE-099 | 79.99 | 26.40 | 0 | 150 | 28.59 | 28.59 | 0.00 | 0.00 | 121.41 | approve |
| FC-EXCESS-INSURANCE-100 | 79.99 | 26.40 | 0 | 350 | 28.59 | 28.59 | 0.00 | 0.00 | 321.41 | approve |
| FC-EXCESS-INSURANCE-101 | 79.99 | 26.40 | 8.00 | 12.50 | 28.59 | 12.50 | 0.00 | 8.09 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-102 | 79.99 | 26.40 | 8.00 | 65 | 28.59 | 20.59 | 0.00 | 0.00 | 44.41 | approve |
| FC-EXCESS-INSURANCE-103 | 79.99 | 26.40 | 8.00 | 150 | 28.59 | 20.59 | 0.00 | 0.00 | 129.41 | approve |
| FC-EXCESS-INSURANCE-104 | 79.99 | 26.40 | 8.00 | 350 | 28.59 | 20.59 | 0.00 | 0.00 | 329.41 | approve |
| FC-EXCESS-INSURANCE-105 | 79.99 | 26.40 | 36.00 | 12.50 | 28.59 | 0.00 | 7.41 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-106 | 79.99 | 26.40 | 36.00 | 65 | 28.59 | 0.00 | 7.41 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-107 | 79.99 | 26.40 | 36.00 | 150 | 28.59 | 0.00 | 7.41 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-108 | 79.99 | 26.40 | 36.00 | 350 | 28.59 | 0.00 | 7.41 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-109 | 79.99 | 26.40 | 63.99 | 12.50 | 28.59 | 0.00 | 35.40 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-110 | 79.99 | 26.40 | 63.99 | 65 | 28.59 | 0.00 | 35.40 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-111 | 79.99 | 26.40 | 63.99 | 150 | 28.59 | 0.00 | 35.40 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-112 | 79.99 | 26.40 | 63.99 | 350 | 28.59 | 0.00 | 35.40 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-113 | 79.99 | 59.99 | 0 | 12.50 | 0.00 | 0.00 | 0.00 | 0.00 | 12.50 | no eligible remainder |
| FC-EXCESS-INSURANCE-114 | 79.99 | 59.99 | 0 | 65 | 0.00 | 0.00 | 0.00 | 0.00 | 65.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-115 | 79.99 | 59.99 | 0 | 150 | 0.00 | 0.00 | 0.00 | 0.00 | 150.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-116 | 79.99 | 59.99 | 0 | 350 | 0.00 | 0.00 | 0.00 | 0.00 | 350.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-117 | 79.99 | 59.99 | 8.00 | 12.50 | 0.00 | 0.00 | 8.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-118 | 79.99 | 59.99 | 8.00 | 65 | 0.00 | 0.00 | 8.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-119 | 79.99 | 59.99 | 8.00 | 150 | 0.00 | 0.00 | 8.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-120 | 79.99 | 59.99 | 8.00 | 350 | 0.00 | 0.00 | 8.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-121 | 79.99 | 59.99 | 36.00 | 12.50 | 0.00 | 0.00 | 36.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-122 | 79.99 | 59.99 | 36.00 | 65 | 0.00 | 0.00 | 36.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-123 | 79.99 | 59.99 | 36.00 | 150 | 0.00 | 0.00 | 36.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-124 | 79.99 | 59.99 | 36.00 | 350 | 0.00 | 0.00 | 36.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-125 | 79.99 | 59.99 | 63.99 | 12.50 | 0.00 | 0.00 | 63.99 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-126 | 79.99 | 59.99 | 63.99 | 65 | 0.00 | 0.00 | 63.99 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-127 | 79.99 | 59.99 | 63.99 | 150 | 0.00 | 0.00 | 63.99 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-128 | 79.99 | 59.99 | 63.99 | 350 | 0.00 | 0.00 | 63.99 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-129 | 125 | 0.00 | 0 | 12.50 | 100.00 | 12.50 | 0.00 | 87.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-130 | 125 | 0.00 | 0 | 65 | 100.00 | 65.00 | 0.00 | 35.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-131 | 125 | 0.00 | 0 | 150 | 100.00 | 100.00 | 0.00 | 0.00 | 50.00 | approve |
| FC-EXCESS-INSURANCE-132 | 125 | 0.00 | 0 | 350 | 100.00 | 100.00 | 0.00 | 0.00 | 250.00 | approve |
| FC-EXCESS-INSURANCE-133 | 125 | 0.00 | 12.50 | 12.50 | 100.00 | 12.50 | 0.00 | 75.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-134 | 125 | 0.00 | 12.50 | 65 | 100.00 | 65.00 | 0.00 | 22.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-135 | 125 | 0.00 | 12.50 | 150 | 100.00 | 87.50 | 0.00 | 0.00 | 62.50 | approve |
| FC-EXCESS-INSURANCE-136 | 125 | 0.00 | 12.50 | 350 | 100.00 | 87.50 | 0.00 | 0.00 | 262.50 | approve |
| FC-EXCESS-INSURANCE-137 | 125 | 0.00 | 56.25 | 12.50 | 100.00 | 12.50 | 0.00 | 31.25 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-138 | 125 | 0.00 | 56.25 | 65 | 100.00 | 43.75 | 0.00 | 0.00 | 21.25 | approve |
| FC-EXCESS-INSURANCE-139 | 125 | 0.00 | 56.25 | 150 | 100.00 | 43.75 | 0.00 | 0.00 | 106.25 | approve |
| FC-EXCESS-INSURANCE-140 | 125 | 0.00 | 56.25 | 350 | 100.00 | 43.75 | 0.00 | 0.00 | 306.25 | approve |
| FC-EXCESS-INSURANCE-141 | 125 | 0.00 | 100.00 | 12.50 | 100.00 | 0.00 | 0.00 | 0.00 | 12.50 | no eligible remainder |
| FC-EXCESS-INSURANCE-142 | 125 | 0.00 | 100.00 | 65 | 100.00 | 0.00 | 0.00 | 0.00 | 65.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-143 | 125 | 0.00 | 100.00 | 150 | 100.00 | 0.00 | 0.00 | 0.00 | 150.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-144 | 125 | 0.00 | 100.00 | 350 | 100.00 | 0.00 | 0.00 | 0.00 | 350.00 | no eligible remainder |
| FC-EXCESS-INSURANCE-145 | 125 | 15.63 | 0 | 12.50 | 84.37 | 12.50 | 0.00 | 71.87 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-146 | 125 | 15.63 | 0 | 65 | 84.37 | 65.00 | 0.00 | 19.37 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-147 | 125 | 15.63 | 0 | 150 | 84.37 | 84.37 | 0.00 | 0.00 | 65.63 | approve |
| FC-EXCESS-INSURANCE-148 | 125 | 15.63 | 0 | 350 | 84.37 | 84.37 | 0.00 | 0.00 | 265.63 | approve |
| FC-EXCESS-INSURANCE-149 | 125 | 15.63 | 12.50 | 12.50 | 84.37 | 12.50 | 0.00 | 59.37 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-150 | 125 | 15.63 | 12.50 | 65 | 84.37 | 65.00 | 0.00 | 6.87 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-151 | 125 | 15.63 | 12.50 | 150 | 84.37 | 71.87 | 0.00 | 0.00 | 78.13 | approve |
| FC-EXCESS-INSURANCE-152 | 125 | 15.63 | 12.50 | 350 | 84.37 | 71.87 | 0.00 | 0.00 | 278.13 | approve |
| FC-EXCESS-INSURANCE-153 | 125 | 15.63 | 56.25 | 12.50 | 84.37 | 12.50 | 0.00 | 15.62 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-154 | 125 | 15.63 | 56.25 | 65 | 84.37 | 28.12 | 0.00 | 0.00 | 36.88 | approve |
| FC-EXCESS-INSURANCE-155 | 125 | 15.63 | 56.25 | 150 | 84.37 | 28.12 | 0.00 | 0.00 | 121.88 | approve |
| FC-EXCESS-INSURANCE-156 | 125 | 15.63 | 56.25 | 350 | 84.37 | 28.12 | 0.00 | 0.00 | 321.88 | approve |
| FC-EXCESS-INSURANCE-157 | 125 | 15.63 | 100.00 | 12.50 | 84.37 | 0.00 | 15.63 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-158 | 125 | 15.63 | 100.00 | 65 | 84.37 | 0.00 | 15.63 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-159 | 125 | 15.63 | 100.00 | 150 | 84.37 | 0.00 | 15.63 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-160 | 125 | 15.63 | 100.00 | 350 | 84.37 | 0.00 | 15.63 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-161 | 125 | 41.25 | 0 | 12.50 | 58.75 | 12.50 | 0.00 | 46.25 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-162 | 125 | 41.25 | 0 | 65 | 58.75 | 58.75 | 0.00 | 0.00 | 6.25 | approve |
| FC-EXCESS-INSURANCE-163 | 125 | 41.25 | 0 | 150 | 58.75 | 58.75 | 0.00 | 0.00 | 91.25 | approve |
| FC-EXCESS-INSURANCE-164 | 125 | 41.25 | 0 | 350 | 58.75 | 58.75 | 0.00 | 0.00 | 291.25 | approve |
| FC-EXCESS-INSURANCE-165 | 125 | 41.25 | 12.50 | 12.50 | 58.75 | 12.50 | 0.00 | 33.75 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-166 | 125 | 41.25 | 12.50 | 65 | 58.75 | 46.25 | 0.00 | 0.00 | 18.75 | approve |
| FC-EXCESS-INSURANCE-167 | 125 | 41.25 | 12.50 | 150 | 58.75 | 46.25 | 0.00 | 0.00 | 103.75 | approve |
| FC-EXCESS-INSURANCE-168 | 125 | 41.25 | 12.50 | 350 | 58.75 | 46.25 | 0.00 | 0.00 | 303.75 | approve |
| FC-EXCESS-INSURANCE-169 | 125 | 41.25 | 56.25 | 12.50 | 58.75 | 2.50 | 0.00 | 0.00 | 10.00 | approve |
| FC-EXCESS-INSURANCE-170 | 125 | 41.25 | 56.25 | 65 | 58.75 | 2.50 | 0.00 | 0.00 | 62.50 | approve |
| FC-EXCESS-INSURANCE-171 | 125 | 41.25 | 56.25 | 150 | 58.75 | 2.50 | 0.00 | 0.00 | 147.50 | approve |
| FC-EXCESS-INSURANCE-172 | 125 | 41.25 | 56.25 | 350 | 58.75 | 2.50 | 0.00 | 0.00 | 347.50 | approve |
| FC-EXCESS-INSURANCE-173 | 125 | 41.25 | 100.00 | 12.50 | 58.75 | 0.00 | 41.25 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-174 | 125 | 41.25 | 100.00 | 65 | 58.75 | 0.00 | 41.25 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-175 | 125 | 41.25 | 100.00 | 150 | 58.75 | 0.00 | 41.25 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-176 | 125 | 41.25 | 100.00 | 350 | 58.75 | 0.00 | 41.25 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-177 | 125 | 93.75 | 0 | 12.50 | 6.25 | 6.25 | 0.00 | 0.00 | 6.25 | approve |
| FC-EXCESS-INSURANCE-178 | 125 | 93.75 | 0 | 65 | 6.25 | 6.25 | 0.00 | 0.00 | 58.75 | approve |
| FC-EXCESS-INSURANCE-179 | 125 | 93.75 | 0 | 150 | 6.25 | 6.25 | 0.00 | 0.00 | 143.75 | approve |
| FC-EXCESS-INSURANCE-180 | 125 | 93.75 | 0 | 350 | 6.25 | 6.25 | 0.00 | 0.00 | 343.75 | approve |
| FC-EXCESS-INSURANCE-181 | 125 | 93.75 | 12.50 | 12.50 | 6.25 | 0.00 | 6.25 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-182 | 125 | 93.75 | 12.50 | 65 | 6.25 | 0.00 | 6.25 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-183 | 125 | 93.75 | 12.50 | 150 | 6.25 | 0.00 | 6.25 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-184 | 125 | 93.75 | 12.50 | 350 | 6.25 | 0.00 | 6.25 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-185 | 125 | 93.75 | 56.25 | 12.50 | 6.25 | 0.00 | 50.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-186 | 125 | 93.75 | 56.25 | 65 | 6.25 | 0.00 | 50.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-187 | 125 | 93.75 | 56.25 | 150 | 6.25 | 0.00 | 50.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-188 | 125 | 93.75 | 56.25 | 350 | 6.25 | 0.00 | 50.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-189 | 125 | 93.75 | 100.00 | 12.50 | 6.25 | 0.00 | 93.75 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-190 | 125 | 93.75 | 100.00 | 65 | 6.25 | 0.00 | 93.75 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-191 | 125 | 93.75 | 100.00 | 150 | 6.25 | 0.00 | 93.75 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-192 | 125 | 93.75 | 100.00 | 350 | 6.25 | 0.00 | 93.75 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-193 | 167.83 | 0.00 | 0 | 12.50 | 142.83 | 12.50 | 0.00 | 130.33 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-194 | 167.83 | 0.00 | 0 | 65 | 142.83 | 65.00 | 0.00 | 77.83 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-195 | 167.83 | 0.00 | 0 | 150 | 142.83 | 142.83 | 0.00 | 0.00 | 7.17 | approve |
| FC-EXCESS-INSURANCE-196 | 167.83 | 0.00 | 0 | 350 | 142.83 | 142.83 | 0.00 | 0.00 | 207.17 | approve |
| FC-EXCESS-INSURANCE-197 | 167.83 | 0.00 | 16.78 | 12.50 | 142.83 | 12.50 | 0.00 | 113.55 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-198 | 167.83 | 0.00 | 16.78 | 65 | 142.83 | 65.00 | 0.00 | 61.05 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-199 | 167.83 | 0.00 | 16.78 | 150 | 142.83 | 126.05 | 0.00 | 0.00 | 23.95 | approve |
| FC-EXCESS-INSURANCE-200 | 167.83 | 0.00 | 16.78 | 350 | 142.83 | 126.05 | 0.00 | 0.00 | 223.95 | approve |
| FC-EXCESS-INSURANCE-201 | 167.83 | 0.00 | 75.52 | 12.50 | 142.83 | 12.50 | 0.00 | 54.81 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-202 | 167.83 | 0.00 | 75.52 | 65 | 142.83 | 65.00 | 0.00 | 2.31 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-203 | 167.83 | 0.00 | 75.52 | 150 | 142.83 | 67.31 | 0.00 | 0.00 | 82.69 | approve |
| FC-EXCESS-INSURANCE-204 | 167.83 | 0.00 | 75.52 | 350 | 142.83 | 67.31 | 0.00 | 0.00 | 282.69 | approve |
| FC-EXCESS-INSURANCE-205 | 167.83 | 0.00 | 134.26 | 12.50 | 142.83 | 8.57 | 0.00 | 0.00 | 3.93 | approve |
| FC-EXCESS-INSURANCE-206 | 167.83 | 0.00 | 134.26 | 65 | 142.83 | 8.57 | 0.00 | 0.00 | 56.43 | approve |
| FC-EXCESS-INSURANCE-207 | 167.83 | 0.00 | 134.26 | 150 | 142.83 | 8.57 | 0.00 | 0.00 | 141.43 | approve |
| FC-EXCESS-INSURANCE-208 | 167.83 | 0.00 | 134.26 | 350 | 142.83 | 8.57 | 0.00 | 0.00 | 341.43 | approve |
| FC-EXCESS-INSURANCE-209 | 167.83 | 20.98 | 0 | 12.50 | 121.85 | 12.50 | 0.00 | 109.35 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-210 | 167.83 | 20.98 | 0 | 65 | 121.85 | 65.00 | 0.00 | 56.85 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-211 | 167.83 | 20.98 | 0 | 150 | 121.85 | 121.85 | 0.00 | 0.00 | 28.15 | approve |
| FC-EXCESS-INSURANCE-212 | 167.83 | 20.98 | 0 | 350 | 121.85 | 121.85 | 0.00 | 0.00 | 228.15 | approve |
| FC-EXCESS-INSURANCE-213 | 167.83 | 20.98 | 16.78 | 12.50 | 121.85 | 12.50 | 0.00 | 92.57 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-214 | 167.83 | 20.98 | 16.78 | 65 | 121.85 | 65.00 | 0.00 | 40.07 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-215 | 167.83 | 20.98 | 16.78 | 150 | 121.85 | 105.07 | 0.00 | 0.00 | 44.93 | approve |
| FC-EXCESS-INSURANCE-216 | 167.83 | 20.98 | 16.78 | 350 | 121.85 | 105.07 | 0.00 | 0.00 | 244.93 | approve |
| FC-EXCESS-INSURANCE-217 | 167.83 | 20.98 | 75.52 | 12.50 | 121.85 | 12.50 | 0.00 | 33.83 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-218 | 167.83 | 20.98 | 75.52 | 65 | 121.85 | 46.33 | 0.00 | 0.00 | 18.67 | approve |
| FC-EXCESS-INSURANCE-219 | 167.83 | 20.98 | 75.52 | 150 | 121.85 | 46.33 | 0.00 | 0.00 | 103.67 | approve |
| FC-EXCESS-INSURANCE-220 | 167.83 | 20.98 | 75.52 | 350 | 121.85 | 46.33 | 0.00 | 0.00 | 303.67 | approve |
| FC-EXCESS-INSURANCE-221 | 167.83 | 20.98 | 134.26 | 12.50 | 121.85 | 0.00 | 12.41 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-222 | 167.83 | 20.98 | 134.26 | 65 | 121.85 | 0.00 | 12.41 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-223 | 167.83 | 20.98 | 134.26 | 150 | 121.85 | 0.00 | 12.41 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-224 | 167.83 | 20.98 | 134.26 | 350 | 121.85 | 0.00 | 12.41 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-225 | 167.83 | 55.38 | 0 | 12.50 | 87.45 | 12.50 | 0.00 | 74.95 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-226 | 167.83 | 55.38 | 0 | 65 | 87.45 | 65.00 | 0.00 | 22.45 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-227 | 167.83 | 55.38 | 0 | 150 | 87.45 | 87.45 | 0.00 | 0.00 | 62.55 | approve |
| FC-EXCESS-INSURANCE-228 | 167.83 | 55.38 | 0 | 350 | 87.45 | 87.45 | 0.00 | 0.00 | 262.55 | approve |
| FC-EXCESS-INSURANCE-229 | 167.83 | 55.38 | 16.78 | 12.50 | 87.45 | 12.50 | 0.00 | 58.17 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-230 | 167.83 | 55.38 | 16.78 | 65 | 87.45 | 65.00 | 0.00 | 5.67 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-231 | 167.83 | 55.38 | 16.78 | 150 | 87.45 | 70.67 | 0.00 | 0.00 | 79.33 | approve |
| FC-EXCESS-INSURANCE-232 | 167.83 | 55.38 | 16.78 | 350 | 87.45 | 70.67 | 0.00 | 0.00 | 279.33 | approve |
| FC-EXCESS-INSURANCE-233 | 167.83 | 55.38 | 75.52 | 12.50 | 87.45 | 11.93 | 0.00 | 0.00 | 0.57 | approve |
| FC-EXCESS-INSURANCE-234 | 167.83 | 55.38 | 75.52 | 65 | 87.45 | 11.93 | 0.00 | 0.00 | 53.07 | approve |
| FC-EXCESS-INSURANCE-235 | 167.83 | 55.38 | 75.52 | 150 | 87.45 | 11.93 | 0.00 | 0.00 | 138.07 | approve |
| FC-EXCESS-INSURANCE-236 | 167.83 | 55.38 | 75.52 | 350 | 87.45 | 11.93 | 0.00 | 0.00 | 338.07 | approve |
| FC-EXCESS-INSURANCE-237 | 167.83 | 55.38 | 134.26 | 12.50 | 87.45 | 0.00 | 46.81 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-238 | 167.83 | 55.38 | 134.26 | 65 | 87.45 | 0.00 | 46.81 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-239 | 167.83 | 55.38 | 134.26 | 150 | 87.45 | 0.00 | 46.81 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-240 | 167.83 | 55.38 | 134.26 | 350 | 87.45 | 0.00 | 46.81 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-241 | 167.83 | 125.87 | 0 | 12.50 | 16.96 | 12.50 | 0.00 | 4.46 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-242 | 167.83 | 125.87 | 0 | 65 | 16.96 | 16.96 | 0.00 | 0.00 | 48.04 | approve |
| FC-EXCESS-INSURANCE-243 | 167.83 | 125.87 | 0 | 150 | 16.96 | 16.96 | 0.00 | 0.00 | 133.04 | approve |
| FC-EXCESS-INSURANCE-244 | 167.83 | 125.87 | 0 | 350 | 16.96 | 16.96 | 0.00 | 0.00 | 333.04 | approve |
| FC-EXCESS-INSURANCE-245 | 167.83 | 125.87 | 16.78 | 12.50 | 16.96 | 0.18 | 0.00 | 0.00 | 12.32 | approve |
| FC-EXCESS-INSURANCE-246 | 167.83 | 125.87 | 16.78 | 65 | 16.96 | 0.18 | 0.00 | 0.00 | 64.82 | approve |
| FC-EXCESS-INSURANCE-247 | 167.83 | 125.87 | 16.78 | 150 | 16.96 | 0.18 | 0.00 | 0.00 | 149.82 | approve |
| FC-EXCESS-INSURANCE-248 | 167.83 | 125.87 | 16.78 | 350 | 16.96 | 0.18 | 0.00 | 0.00 | 349.82 | approve |
| FC-EXCESS-INSURANCE-249 | 167.83 | 125.87 | 75.52 | 12.50 | 16.96 | 0.00 | 58.56 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-250 | 167.83 | 125.87 | 75.52 | 65 | 16.96 | 0.00 | 58.56 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-251 | 167.83 | 125.87 | 75.52 | 150 | 16.96 | 0.00 | 58.56 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-252 | 167.83 | 125.87 | 75.52 | 350 | 16.96 | 0.00 | 58.56 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-253 | 167.83 | 125.87 | 134.26 | 12.50 | 16.96 | 0.00 | 117.30 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-254 | 167.83 | 125.87 | 134.26 | 65 | 16.96 | 0.00 | 117.30 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-255 | 167.83 | 125.87 | 134.26 | 150 | 16.96 | 0.00 | 117.30 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-256 | 167.83 | 125.87 | 134.26 | 350 | 16.96 | 0.00 | 117.30 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-257 | 320 | 0.00 | 0 | 12.50 | 295.00 | 12.50 | 0.00 | 282.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-258 | 320 | 0.00 | 0 | 65 | 295.00 | 65.00 | 0.00 | 230.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-259 | 320 | 0.00 | 0 | 150 | 295.00 | 150.00 | 0.00 | 145.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-260 | 320 | 0.00 | 0 | 350 | 295.00 | 295.00 | 0.00 | 0.00 | 55.00 | approve |
| FC-EXCESS-INSURANCE-261 | 320 | 0.00 | 32.00 | 12.50 | 295.00 | 12.50 | 0.00 | 250.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-262 | 320 | 0.00 | 32.00 | 65 | 295.00 | 65.00 | 0.00 | 198.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-263 | 320 | 0.00 | 32.00 | 150 | 295.00 | 150.00 | 0.00 | 113.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-264 | 320 | 0.00 | 32.00 | 350 | 295.00 | 263.00 | 0.00 | 0.00 | 87.00 | approve |
| FC-EXCESS-INSURANCE-265 | 320 | 0.00 | 144.00 | 12.50 | 295.00 | 12.50 | 0.00 | 138.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-266 | 320 | 0.00 | 144.00 | 65 | 295.00 | 65.00 | 0.00 | 86.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-267 | 320 | 0.00 | 144.00 | 150 | 295.00 | 150.00 | 0.00 | 1.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-268 | 320 | 0.00 | 144.00 | 350 | 295.00 | 151.00 | 0.00 | 0.00 | 199.00 | approve |
| FC-EXCESS-INSURANCE-269 | 320 | 0.00 | 256.00 | 12.50 | 295.00 | 12.50 | 0.00 | 26.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-270 | 320 | 0.00 | 256.00 | 65 | 295.00 | 39.00 | 0.00 | 0.00 | 26.00 | approve |
| FC-EXCESS-INSURANCE-271 | 320 | 0.00 | 256.00 | 150 | 295.00 | 39.00 | 0.00 | 0.00 | 111.00 | approve |
| FC-EXCESS-INSURANCE-272 | 320 | 0.00 | 256.00 | 350 | 295.00 | 39.00 | 0.00 | 0.00 | 311.00 | approve |
| FC-EXCESS-INSURANCE-273 | 320 | 40.00 | 0 | 12.50 | 255.00 | 12.50 | 0.00 | 242.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-274 | 320 | 40.00 | 0 | 65 | 255.00 | 65.00 | 0.00 | 190.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-275 | 320 | 40.00 | 0 | 150 | 255.00 | 150.00 | 0.00 | 105.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-276 | 320 | 40.00 | 0 | 350 | 255.00 | 255.00 | 0.00 | 0.00 | 95.00 | approve |
| FC-EXCESS-INSURANCE-277 | 320 | 40.00 | 32.00 | 12.50 | 255.00 | 12.50 | 0.00 | 210.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-278 | 320 | 40.00 | 32.00 | 65 | 255.00 | 65.00 | 0.00 | 158.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-279 | 320 | 40.00 | 32.00 | 150 | 255.00 | 150.00 | 0.00 | 73.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-280 | 320 | 40.00 | 32.00 | 350 | 255.00 | 223.00 | 0.00 | 0.00 | 127.00 | approve |
| FC-EXCESS-INSURANCE-281 | 320 | 40.00 | 144.00 | 12.50 | 255.00 | 12.50 | 0.00 | 98.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-282 | 320 | 40.00 | 144.00 | 65 | 255.00 | 65.00 | 0.00 | 46.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-283 | 320 | 40.00 | 144.00 | 150 | 255.00 | 111.00 | 0.00 | 0.00 | 39.00 | approve |
| FC-EXCESS-INSURANCE-284 | 320 | 40.00 | 144.00 | 350 | 255.00 | 111.00 | 0.00 | 0.00 | 239.00 | approve |
| FC-EXCESS-INSURANCE-285 | 320 | 40.00 | 256.00 | 12.50 | 255.00 | 0.00 | 1.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-286 | 320 | 40.00 | 256.00 | 65 | 255.00 | 0.00 | 1.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-287 | 320 | 40.00 | 256.00 | 150 | 255.00 | 0.00 | 1.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-288 | 320 | 40.00 | 256.00 | 350 | 255.00 | 0.00 | 1.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-289 | 320 | 105.60 | 0 | 12.50 | 189.40 | 12.50 | 0.00 | 176.90 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-290 | 320 | 105.60 | 0 | 65 | 189.40 | 65.00 | 0.00 | 124.40 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-291 | 320 | 105.60 | 0 | 150 | 189.40 | 150.00 | 0.00 | 39.40 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-292 | 320 | 105.60 | 0 | 350 | 189.40 | 189.40 | 0.00 | 0.00 | 160.60 | approve |
| FC-EXCESS-INSURANCE-293 | 320 | 105.60 | 32.00 | 12.50 | 189.40 | 12.50 | 0.00 | 144.90 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-294 | 320 | 105.60 | 32.00 | 65 | 189.40 | 65.00 | 0.00 | 92.40 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-295 | 320 | 105.60 | 32.00 | 150 | 189.40 | 150.00 | 0.00 | 7.40 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-296 | 320 | 105.60 | 32.00 | 350 | 189.40 | 157.40 | 0.00 | 0.00 | 192.60 | approve |
| FC-EXCESS-INSURANCE-297 | 320 | 105.60 | 144.00 | 12.50 | 189.40 | 12.50 | 0.00 | 32.90 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-298 | 320 | 105.60 | 144.00 | 65 | 189.40 | 45.40 | 0.00 | 0.00 | 19.60 | approve |
| FC-EXCESS-INSURANCE-299 | 320 | 105.60 | 144.00 | 150 | 189.40 | 45.40 | 0.00 | 0.00 | 104.60 | approve |
| FC-EXCESS-INSURANCE-300 | 320 | 105.60 | 144.00 | 350 | 189.40 | 45.40 | 0.00 | 0.00 | 304.60 | approve |
| FC-EXCESS-INSURANCE-301 | 320 | 105.60 | 256.00 | 12.50 | 189.40 | 0.00 | 66.60 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-302 | 320 | 105.60 | 256.00 | 65 | 189.40 | 0.00 | 66.60 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-303 | 320 | 105.60 | 256.00 | 150 | 189.40 | 0.00 | 66.60 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-304 | 320 | 105.60 | 256.00 | 350 | 189.40 | 0.00 | 66.60 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-305 | 320 | 240.00 | 0 | 12.50 | 55.00 | 12.50 | 0.00 | 42.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-306 | 320 | 240.00 | 0 | 65 | 55.00 | 55.00 | 0.00 | 0.00 | 10.00 | approve |
| FC-EXCESS-INSURANCE-307 | 320 | 240.00 | 0 | 150 | 55.00 | 55.00 | 0.00 | 0.00 | 95.00 | approve |
| FC-EXCESS-INSURANCE-308 | 320 | 240.00 | 0 | 350 | 55.00 | 55.00 | 0.00 | 0.00 | 295.00 | approve |
| FC-EXCESS-INSURANCE-309 | 320 | 240.00 | 32.00 | 12.50 | 55.00 | 12.50 | 0.00 | 10.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-310 | 320 | 240.00 | 32.00 | 65 | 55.00 | 23.00 | 0.00 | 0.00 | 42.00 | approve |
| FC-EXCESS-INSURANCE-311 | 320 | 240.00 | 32.00 | 150 | 55.00 | 23.00 | 0.00 | 0.00 | 127.00 | approve |
| FC-EXCESS-INSURANCE-312 | 320 | 240.00 | 32.00 | 350 | 55.00 | 23.00 | 0.00 | 0.00 | 327.00 | approve |
| FC-EXCESS-INSURANCE-313 | 320 | 240.00 | 144.00 | 12.50 | 55.00 | 0.00 | 89.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-314 | 320 | 240.00 | 144.00 | 65 | 55.00 | 0.00 | 89.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-315 | 320 | 240.00 | 144.00 | 150 | 55.00 | 0.00 | 89.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-316 | 320 | 240.00 | 144.00 | 350 | 55.00 | 0.00 | 89.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-317 | 320 | 240.00 | 256.00 | 12.50 | 55.00 | 0.00 | 201.00 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-318 | 320 | 240.00 | 256.00 | 65 | 55.00 | 0.00 | 201.00 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-319 | 320 | 240.00 | 256.00 | 150 | 55.00 | 0.00 | 201.00 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-320 | 320 | 240.00 | 256.00 | 350 | 55.00 | 0.00 | 201.00 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-321 | 725.50 | 0.00 | 0 | 12.50 | 700.50 | 12.50 | 0.00 | 688.00 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-322 | 725.50 | 0.00 | 0 | 65 | 700.50 | 65.00 | 0.00 | 635.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-323 | 725.50 | 0.00 | 0 | 150 | 700.50 | 150.00 | 0.00 | 550.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-324 | 725.50 | 0.00 | 0 | 350 | 700.50 | 350.00 | 0.00 | 350.50 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-325 | 725.50 | 0.00 | 72.55 | 12.50 | 700.50 | 12.50 | 0.00 | 615.45 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-326 | 725.50 | 0.00 | 72.55 | 65 | 700.50 | 65.00 | 0.00 | 562.95 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-327 | 725.50 | 0.00 | 72.55 | 150 | 700.50 | 150.00 | 0.00 | 477.95 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-328 | 725.50 | 0.00 | 72.55 | 350 | 700.50 | 350.00 | 0.00 | 277.95 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-329 | 725.50 | 0.00 | 326.48 | 12.50 | 700.50 | 12.50 | 0.00 | 361.52 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-330 | 725.50 | 0.00 | 326.48 | 65 | 700.50 | 65.00 | 0.00 | 309.02 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-331 | 725.50 | 0.00 | 326.48 | 150 | 700.50 | 150.00 | 0.00 | 224.02 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-332 | 725.50 | 0.00 | 326.48 | 350 | 700.50 | 350.00 | 0.00 | 24.02 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-333 | 725.50 | 0.00 | 580.40 | 12.50 | 700.50 | 12.50 | 0.00 | 107.60 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-334 | 725.50 | 0.00 | 580.40 | 65 | 700.50 | 65.00 | 0.00 | 55.10 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-335 | 725.50 | 0.00 | 580.40 | 150 | 700.50 | 120.10 | 0.00 | 0.00 | 29.90 | approve |
| FC-EXCESS-INSURANCE-336 | 725.50 | 0.00 | 580.40 | 350 | 700.50 | 120.10 | 0.00 | 0.00 | 229.90 | approve |
| FC-EXCESS-INSURANCE-337 | 725.50 | 90.69 | 0 | 12.50 | 609.81 | 12.50 | 0.00 | 597.31 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-338 | 725.50 | 90.69 | 0 | 65 | 609.81 | 65.00 | 0.00 | 544.81 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-339 | 725.50 | 90.69 | 0 | 150 | 609.81 | 150.00 | 0.00 | 459.81 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-340 | 725.50 | 90.69 | 0 | 350 | 609.81 | 350.00 | 0.00 | 259.81 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-341 | 725.50 | 90.69 | 72.55 | 12.50 | 609.81 | 12.50 | 0.00 | 524.76 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-342 | 725.50 | 90.69 | 72.55 | 65 | 609.81 | 65.00 | 0.00 | 472.26 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-343 | 725.50 | 90.69 | 72.55 | 150 | 609.81 | 150.00 | 0.00 | 387.26 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-344 | 725.50 | 90.69 | 72.55 | 350 | 609.81 | 350.00 | 0.00 | 187.26 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-345 | 725.50 | 90.69 | 326.48 | 12.50 | 609.81 | 12.50 | 0.00 | 270.83 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-346 | 725.50 | 90.69 | 326.48 | 65 | 609.81 | 65.00 | 0.00 | 218.33 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-347 | 725.50 | 90.69 | 326.48 | 150 | 609.81 | 150.00 | 0.00 | 133.33 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-348 | 725.50 | 90.69 | 326.48 | 350 | 609.81 | 283.33 | 0.00 | 0.00 | 66.67 | approve |
| FC-EXCESS-INSURANCE-349 | 725.50 | 90.69 | 580.40 | 12.50 | 609.81 | 12.50 | 0.00 | 16.91 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-350 | 725.50 | 90.69 | 580.40 | 65 | 609.81 | 29.41 | 0.00 | 0.00 | 35.59 | approve |
| FC-EXCESS-INSURANCE-351 | 725.50 | 90.69 | 580.40 | 150 | 609.81 | 29.41 | 0.00 | 0.00 | 120.59 | approve |
| FC-EXCESS-INSURANCE-352 | 725.50 | 90.69 | 580.40 | 350 | 609.81 | 29.41 | 0.00 | 0.00 | 320.59 | approve |
| FC-EXCESS-INSURANCE-353 | 725.50 | 239.42 | 0 | 12.50 | 461.08 | 12.50 | 0.00 | 448.58 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-354 | 725.50 | 239.42 | 0 | 65 | 461.08 | 65.00 | 0.00 | 396.08 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-355 | 725.50 | 239.42 | 0 | 150 | 461.08 | 150.00 | 0.00 | 311.08 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-356 | 725.50 | 239.42 | 0 | 350 | 461.08 | 350.00 | 0.00 | 111.08 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-357 | 725.50 | 239.42 | 72.55 | 12.50 | 461.08 | 12.50 | 0.00 | 376.03 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-358 | 725.50 | 239.42 | 72.55 | 65 | 461.08 | 65.00 | 0.00 | 323.53 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-359 | 725.50 | 239.42 | 72.55 | 150 | 461.08 | 150.00 | 0.00 | 238.53 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-360 | 725.50 | 239.42 | 72.55 | 350 | 461.08 | 350.00 | 0.00 | 38.53 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-361 | 725.50 | 239.42 | 326.48 | 12.50 | 461.08 | 12.50 | 0.00 | 122.10 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-362 | 725.50 | 239.42 | 326.48 | 65 | 461.08 | 65.00 | 0.00 | 69.60 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-363 | 725.50 | 239.42 | 326.48 | 150 | 461.08 | 134.60 | 0.00 | 0.00 | 15.40 | approve |
| FC-EXCESS-INSURANCE-364 | 725.50 | 239.42 | 326.48 | 350 | 461.08 | 134.60 | 0.00 | 0.00 | 215.40 | approve |
| FC-EXCESS-INSURANCE-365 | 725.50 | 239.42 | 580.40 | 12.50 | 461.08 | 0.00 | 119.32 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-366 | 725.50 | 239.42 | 580.40 | 65 | 461.08 | 0.00 | 119.32 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-367 | 725.50 | 239.42 | 580.40 | 150 | 461.08 | 0.00 | 119.32 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-368 | 725.50 | 239.42 | 580.40 | 350 | 461.08 | 0.00 | 119.32 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-369 | 725.50 | 544.13 | 0 | 12.50 | 156.37 | 12.50 | 0.00 | 143.87 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-370 | 725.50 | 544.13 | 0 | 65 | 156.37 | 65.00 | 0.00 | 91.37 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-371 | 725.50 | 544.13 | 0 | 150 | 156.37 | 150.00 | 0.00 | 6.37 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-372 | 725.50 | 544.13 | 0 | 350 | 156.37 | 156.37 | 0.00 | 0.00 | 193.63 | approve |
| FC-EXCESS-INSURANCE-373 | 725.50 | 544.13 | 72.55 | 12.50 | 156.37 | 12.50 | 0.00 | 71.32 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-374 | 725.50 | 544.13 | 72.55 | 65 | 156.37 | 65.00 | 0.00 | 18.82 | 0.00 | ceiling reached |
| FC-EXCESS-INSURANCE-375 | 725.50 | 544.13 | 72.55 | 150 | 156.37 | 83.82 | 0.00 | 0.00 | 66.18 | approve |
| FC-EXCESS-INSURANCE-376 | 725.50 | 544.13 | 72.55 | 350 | 156.37 | 83.82 | 0.00 | 0.00 | 266.18 | approve |
| FC-EXCESS-INSURANCE-377 | 725.50 | 544.13 | 326.48 | 12.50 | 156.37 | 0.00 | 170.11 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-378 | 725.50 | 544.13 | 326.48 | 65 | 156.37 | 0.00 | 170.11 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-379 | 725.50 | 544.13 | 326.48 | 150 | 156.37 | 0.00 | 170.11 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-380 | 725.50 | 544.13 | 326.48 | 350 | 156.37 | 0.00 | 170.11 | 0.00 | 350.00 | recover |
| FC-EXCESS-INSURANCE-381 | 725.50 | 544.13 | 580.40 | 12.50 | 156.37 | 0.00 | 424.03 | 0.00 | 12.50 | recover |
| FC-EXCESS-INSURANCE-382 | 725.50 | 544.13 | 580.40 | 65 | 156.37 | 0.00 | 424.03 | 0.00 | 65.00 | recover |
| FC-EXCESS-INSURANCE-383 | 725.50 | 544.13 | 580.40 | 150 | 156.37 | 0.00 | 424.03 | 0.00 | 150.00 | recover |
| FC-EXCESS-INSURANCE-384 | 725.50 | 544.13 | 580.40 | 350 | 156.37 | 0.00 | 424.03 | 0.00 | 350.00 | recover |

## Reconciliation

Subtract prior claims from cumulative entitlement. A negative result requires a recovery review and never creates a new negative draw. Award remaining decreases exactly by the new claim. Amounts above the remaining award stay visible as unfunded eligible cost. Status alone does not authorize immediate recovery cash.

[Finance decision fixture index](../README.md)
