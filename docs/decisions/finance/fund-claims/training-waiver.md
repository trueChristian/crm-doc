# Training award covers two thirds to a 150 item limit

The officer has an approved eligible supplier cost, a known exclusion, reimbursement already credited to that cost and remaining award ceiling. Reimbursement is 0.6666666667 of (cost less excluded amount less deductible 0, floored at zero), rounded half up; then cap the cumulative reimbursement per cost at 150. Only the still-eligible portion can be claimed up to remaining award. A passed claim under this reimbursement policy debits grant receivable and credits grant income if earning and claim approval coincide. Recovery is a review amount on a prior claim, awaiting the authorized credit/repayment decision.

Read the input columns left to right. All amounts are in the stated book currency, at two decimal places unless a column identifies foreign units or a rate. Each row is an independent transaction or cutoff. Apply the stated local policy before comparing your result.

| Case | Original cost | Excluded cost | Already claimed | Award left before | Earned cumul. | New claim Dr/Cr | Review recovery | Earned over ceiling | Award left after | Decision |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FC-TRAINING-WAIVER-001 | 31.25 | 0.00 | 0 | 12.50 | 20.83 | 12.50 | 0.00 | 8.33 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-002 | 31.25 | 0.00 | 0 | 65 | 20.83 | 20.83 | 0.00 | 0.00 | 44.17 | approve |
| FC-TRAINING-WAIVER-003 | 31.25 | 0.00 | 0 | 150 | 20.83 | 20.83 | 0.00 | 0.00 | 129.17 | approve |
| FC-TRAINING-WAIVER-004 | 31.25 | 0.00 | 0 | 350 | 20.83 | 20.83 | 0.00 | 0.00 | 329.17 | approve |
| FC-TRAINING-WAIVER-005 | 31.25 | 0.00 | 3.13 | 12.50 | 20.83 | 12.50 | 0.00 | 5.20 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-006 | 31.25 | 0.00 | 3.13 | 65 | 20.83 | 17.70 | 0.00 | 0.00 | 47.30 | approve |
| FC-TRAINING-WAIVER-007 | 31.25 | 0.00 | 3.13 | 150 | 20.83 | 17.70 | 0.00 | 0.00 | 132.30 | approve |
| FC-TRAINING-WAIVER-008 | 31.25 | 0.00 | 3.13 | 350 | 20.83 | 17.70 | 0.00 | 0.00 | 332.30 | approve |
| FC-TRAINING-WAIVER-009 | 31.25 | 0.00 | 14.06 | 12.50 | 20.83 | 6.77 | 0.00 | 0.00 | 5.73 | approve |
| FC-TRAINING-WAIVER-010 | 31.25 | 0.00 | 14.06 | 65 | 20.83 | 6.77 | 0.00 | 0.00 | 58.23 | approve |
| FC-TRAINING-WAIVER-011 | 31.25 | 0.00 | 14.06 | 150 | 20.83 | 6.77 | 0.00 | 0.00 | 143.23 | approve |
| FC-TRAINING-WAIVER-012 | 31.25 | 0.00 | 14.06 | 350 | 20.83 | 6.77 | 0.00 | 0.00 | 343.23 | approve |
| FC-TRAINING-WAIVER-013 | 31.25 | 0.00 | 25.00 | 12.50 | 20.83 | 0.00 | 4.17 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-014 | 31.25 | 0.00 | 25.00 | 65 | 20.83 | 0.00 | 4.17 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-015 | 31.25 | 0.00 | 25.00 | 150 | 20.83 | 0.00 | 4.17 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-016 | 31.25 | 0.00 | 25.00 | 350 | 20.83 | 0.00 | 4.17 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-017 | 31.25 | 3.91 | 0 | 12.50 | 18.23 | 12.50 | 0.00 | 5.73 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-018 | 31.25 | 3.91 | 0 | 65 | 18.23 | 18.23 | 0.00 | 0.00 | 46.77 | approve |
| FC-TRAINING-WAIVER-019 | 31.25 | 3.91 | 0 | 150 | 18.23 | 18.23 | 0.00 | 0.00 | 131.77 | approve |
| FC-TRAINING-WAIVER-020 | 31.25 | 3.91 | 0 | 350 | 18.23 | 18.23 | 0.00 | 0.00 | 331.77 | approve |
| FC-TRAINING-WAIVER-021 | 31.25 | 3.91 | 3.13 | 12.50 | 18.23 | 12.50 | 0.00 | 2.60 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-022 | 31.25 | 3.91 | 3.13 | 65 | 18.23 | 15.10 | 0.00 | 0.00 | 49.90 | approve |
| FC-TRAINING-WAIVER-023 | 31.25 | 3.91 | 3.13 | 150 | 18.23 | 15.10 | 0.00 | 0.00 | 134.90 | approve |
| FC-TRAINING-WAIVER-024 | 31.25 | 3.91 | 3.13 | 350 | 18.23 | 15.10 | 0.00 | 0.00 | 334.90 | approve |
| FC-TRAINING-WAIVER-025 | 31.25 | 3.91 | 14.06 | 12.50 | 18.23 | 4.17 | 0.00 | 0.00 | 8.33 | approve |
| FC-TRAINING-WAIVER-026 | 31.25 | 3.91 | 14.06 | 65 | 18.23 | 4.17 | 0.00 | 0.00 | 60.83 | approve |
| FC-TRAINING-WAIVER-027 | 31.25 | 3.91 | 14.06 | 150 | 18.23 | 4.17 | 0.00 | 0.00 | 145.83 | approve |
| FC-TRAINING-WAIVER-028 | 31.25 | 3.91 | 14.06 | 350 | 18.23 | 4.17 | 0.00 | 0.00 | 345.83 | approve |
| FC-TRAINING-WAIVER-029 | 31.25 | 3.91 | 25.00 | 12.50 | 18.23 | 0.00 | 6.77 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-030 | 31.25 | 3.91 | 25.00 | 65 | 18.23 | 0.00 | 6.77 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-031 | 31.25 | 3.91 | 25.00 | 150 | 18.23 | 0.00 | 6.77 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-032 | 31.25 | 3.91 | 25.00 | 350 | 18.23 | 0.00 | 6.77 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-033 | 31.25 | 10.31 | 0 | 12.50 | 13.96 | 12.50 | 0.00 | 1.46 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-034 | 31.25 | 10.31 | 0 | 65 | 13.96 | 13.96 | 0.00 | 0.00 | 51.04 | approve |
| FC-TRAINING-WAIVER-035 | 31.25 | 10.31 | 0 | 150 | 13.96 | 13.96 | 0.00 | 0.00 | 136.04 | approve |
| FC-TRAINING-WAIVER-036 | 31.25 | 10.31 | 0 | 350 | 13.96 | 13.96 | 0.00 | 0.00 | 336.04 | approve |
| FC-TRAINING-WAIVER-037 | 31.25 | 10.31 | 3.13 | 12.50 | 13.96 | 10.83 | 0.00 | 0.00 | 1.67 | approve |
| FC-TRAINING-WAIVER-038 | 31.25 | 10.31 | 3.13 | 65 | 13.96 | 10.83 | 0.00 | 0.00 | 54.17 | approve |
| FC-TRAINING-WAIVER-039 | 31.25 | 10.31 | 3.13 | 150 | 13.96 | 10.83 | 0.00 | 0.00 | 139.17 | approve |
| FC-TRAINING-WAIVER-040 | 31.25 | 10.31 | 3.13 | 350 | 13.96 | 10.83 | 0.00 | 0.00 | 339.17 | approve |
| FC-TRAINING-WAIVER-041 | 31.25 | 10.31 | 14.06 | 12.50 | 13.96 | 0.00 | 0.10 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-042 | 31.25 | 10.31 | 14.06 | 65 | 13.96 | 0.00 | 0.10 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-043 | 31.25 | 10.31 | 14.06 | 150 | 13.96 | 0.00 | 0.10 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-044 | 31.25 | 10.31 | 14.06 | 350 | 13.96 | 0.00 | 0.10 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-045 | 31.25 | 10.31 | 25.00 | 12.50 | 13.96 | 0.00 | 11.04 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-046 | 31.25 | 10.31 | 25.00 | 65 | 13.96 | 0.00 | 11.04 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-047 | 31.25 | 10.31 | 25.00 | 150 | 13.96 | 0.00 | 11.04 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-048 | 31.25 | 10.31 | 25.00 | 350 | 13.96 | 0.00 | 11.04 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-049 | 31.25 | 23.44 | 0 | 12.50 | 5.21 | 5.21 | 0.00 | 0.00 | 7.29 | approve |
| FC-TRAINING-WAIVER-050 | 31.25 | 23.44 | 0 | 65 | 5.21 | 5.21 | 0.00 | 0.00 | 59.79 | approve |
| FC-TRAINING-WAIVER-051 | 31.25 | 23.44 | 0 | 150 | 5.21 | 5.21 | 0.00 | 0.00 | 144.79 | approve |
| FC-TRAINING-WAIVER-052 | 31.25 | 23.44 | 0 | 350 | 5.21 | 5.21 | 0.00 | 0.00 | 344.79 | approve |
| FC-TRAINING-WAIVER-053 | 31.25 | 23.44 | 3.13 | 12.50 | 5.21 | 2.08 | 0.00 | 0.00 | 10.42 | approve |
| FC-TRAINING-WAIVER-054 | 31.25 | 23.44 | 3.13 | 65 | 5.21 | 2.08 | 0.00 | 0.00 | 62.92 | approve |
| FC-TRAINING-WAIVER-055 | 31.25 | 23.44 | 3.13 | 150 | 5.21 | 2.08 | 0.00 | 0.00 | 147.92 | approve |
| FC-TRAINING-WAIVER-056 | 31.25 | 23.44 | 3.13 | 350 | 5.21 | 2.08 | 0.00 | 0.00 | 347.92 | approve |
| FC-TRAINING-WAIVER-057 | 31.25 | 23.44 | 14.06 | 12.50 | 5.21 | 0.00 | 8.85 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-058 | 31.25 | 23.44 | 14.06 | 65 | 5.21 | 0.00 | 8.85 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-059 | 31.25 | 23.44 | 14.06 | 150 | 5.21 | 0.00 | 8.85 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-060 | 31.25 | 23.44 | 14.06 | 350 | 5.21 | 0.00 | 8.85 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-061 | 31.25 | 23.44 | 25.00 | 12.50 | 5.21 | 0.00 | 19.79 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-062 | 31.25 | 23.44 | 25.00 | 65 | 5.21 | 0.00 | 19.79 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-063 | 31.25 | 23.44 | 25.00 | 150 | 5.21 | 0.00 | 19.79 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-064 | 31.25 | 23.44 | 25.00 | 350 | 5.21 | 0.00 | 19.79 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-065 | 79.99 | 0.00 | 0 | 12.50 | 53.33 | 12.50 | 0.00 | 40.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-066 | 79.99 | 0.00 | 0 | 65 | 53.33 | 53.33 | 0.00 | 0.00 | 11.67 | approve |
| FC-TRAINING-WAIVER-067 | 79.99 | 0.00 | 0 | 150 | 53.33 | 53.33 | 0.00 | 0.00 | 96.67 | approve |
| FC-TRAINING-WAIVER-068 | 79.99 | 0.00 | 0 | 350 | 53.33 | 53.33 | 0.00 | 0.00 | 296.67 | approve |
| FC-TRAINING-WAIVER-069 | 79.99 | 0.00 | 8.00 | 12.50 | 53.33 | 12.50 | 0.00 | 32.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-070 | 79.99 | 0.00 | 8.00 | 65 | 53.33 | 45.33 | 0.00 | 0.00 | 19.67 | approve |
| FC-TRAINING-WAIVER-071 | 79.99 | 0.00 | 8.00 | 150 | 53.33 | 45.33 | 0.00 | 0.00 | 104.67 | approve |
| FC-TRAINING-WAIVER-072 | 79.99 | 0.00 | 8.00 | 350 | 53.33 | 45.33 | 0.00 | 0.00 | 304.67 | approve |
| FC-TRAINING-WAIVER-073 | 79.99 | 0.00 | 36.00 | 12.50 | 53.33 | 12.50 | 0.00 | 4.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-074 | 79.99 | 0.00 | 36.00 | 65 | 53.33 | 17.33 | 0.00 | 0.00 | 47.67 | approve |
| FC-TRAINING-WAIVER-075 | 79.99 | 0.00 | 36.00 | 150 | 53.33 | 17.33 | 0.00 | 0.00 | 132.67 | approve |
| FC-TRAINING-WAIVER-076 | 79.99 | 0.00 | 36.00 | 350 | 53.33 | 17.33 | 0.00 | 0.00 | 332.67 | approve |
| FC-TRAINING-WAIVER-077 | 79.99 | 0.00 | 63.99 | 12.50 | 53.33 | 0.00 | 10.66 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-078 | 79.99 | 0.00 | 63.99 | 65 | 53.33 | 0.00 | 10.66 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-079 | 79.99 | 0.00 | 63.99 | 150 | 53.33 | 0.00 | 10.66 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-080 | 79.99 | 0.00 | 63.99 | 350 | 53.33 | 0.00 | 10.66 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-081 | 79.99 | 10.00 | 0 | 12.50 | 46.66 | 12.50 | 0.00 | 34.16 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-082 | 79.99 | 10.00 | 0 | 65 | 46.66 | 46.66 | 0.00 | 0.00 | 18.34 | approve |
| FC-TRAINING-WAIVER-083 | 79.99 | 10.00 | 0 | 150 | 46.66 | 46.66 | 0.00 | 0.00 | 103.34 | approve |
| FC-TRAINING-WAIVER-084 | 79.99 | 10.00 | 0 | 350 | 46.66 | 46.66 | 0.00 | 0.00 | 303.34 | approve |
| FC-TRAINING-WAIVER-085 | 79.99 | 10.00 | 8.00 | 12.50 | 46.66 | 12.50 | 0.00 | 26.16 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-086 | 79.99 | 10.00 | 8.00 | 65 | 46.66 | 38.66 | 0.00 | 0.00 | 26.34 | approve |
| FC-TRAINING-WAIVER-087 | 79.99 | 10.00 | 8.00 | 150 | 46.66 | 38.66 | 0.00 | 0.00 | 111.34 | approve |
| FC-TRAINING-WAIVER-088 | 79.99 | 10.00 | 8.00 | 350 | 46.66 | 38.66 | 0.00 | 0.00 | 311.34 | approve |
| FC-TRAINING-WAIVER-089 | 79.99 | 10.00 | 36.00 | 12.50 | 46.66 | 10.66 | 0.00 | 0.00 | 1.84 | approve |
| FC-TRAINING-WAIVER-090 | 79.99 | 10.00 | 36.00 | 65 | 46.66 | 10.66 | 0.00 | 0.00 | 54.34 | approve |
| FC-TRAINING-WAIVER-091 | 79.99 | 10.00 | 36.00 | 150 | 46.66 | 10.66 | 0.00 | 0.00 | 139.34 | approve |
| FC-TRAINING-WAIVER-092 | 79.99 | 10.00 | 36.00 | 350 | 46.66 | 10.66 | 0.00 | 0.00 | 339.34 | approve |
| FC-TRAINING-WAIVER-093 | 79.99 | 10.00 | 63.99 | 12.50 | 46.66 | 0.00 | 17.33 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-094 | 79.99 | 10.00 | 63.99 | 65 | 46.66 | 0.00 | 17.33 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-095 | 79.99 | 10.00 | 63.99 | 150 | 46.66 | 0.00 | 17.33 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-096 | 79.99 | 10.00 | 63.99 | 350 | 46.66 | 0.00 | 17.33 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-097 | 79.99 | 26.40 | 0 | 12.50 | 35.73 | 12.50 | 0.00 | 23.23 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-098 | 79.99 | 26.40 | 0 | 65 | 35.73 | 35.73 | 0.00 | 0.00 | 29.27 | approve |
| FC-TRAINING-WAIVER-099 | 79.99 | 26.40 | 0 | 150 | 35.73 | 35.73 | 0.00 | 0.00 | 114.27 | approve |
| FC-TRAINING-WAIVER-100 | 79.99 | 26.40 | 0 | 350 | 35.73 | 35.73 | 0.00 | 0.00 | 314.27 | approve |
| FC-TRAINING-WAIVER-101 | 79.99 | 26.40 | 8.00 | 12.50 | 35.73 | 12.50 | 0.00 | 15.23 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-102 | 79.99 | 26.40 | 8.00 | 65 | 35.73 | 27.73 | 0.00 | 0.00 | 37.27 | approve |
| FC-TRAINING-WAIVER-103 | 79.99 | 26.40 | 8.00 | 150 | 35.73 | 27.73 | 0.00 | 0.00 | 122.27 | approve |
| FC-TRAINING-WAIVER-104 | 79.99 | 26.40 | 8.00 | 350 | 35.73 | 27.73 | 0.00 | 0.00 | 322.27 | approve |
| FC-TRAINING-WAIVER-105 | 79.99 | 26.40 | 36.00 | 12.50 | 35.73 | 0.00 | 0.27 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-106 | 79.99 | 26.40 | 36.00 | 65 | 35.73 | 0.00 | 0.27 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-107 | 79.99 | 26.40 | 36.00 | 150 | 35.73 | 0.00 | 0.27 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-108 | 79.99 | 26.40 | 36.00 | 350 | 35.73 | 0.00 | 0.27 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-109 | 79.99 | 26.40 | 63.99 | 12.50 | 35.73 | 0.00 | 28.26 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-110 | 79.99 | 26.40 | 63.99 | 65 | 35.73 | 0.00 | 28.26 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-111 | 79.99 | 26.40 | 63.99 | 150 | 35.73 | 0.00 | 28.26 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-112 | 79.99 | 26.40 | 63.99 | 350 | 35.73 | 0.00 | 28.26 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-113 | 79.99 | 59.99 | 0 | 12.50 | 13.33 | 12.50 | 0.00 | 0.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-114 | 79.99 | 59.99 | 0 | 65 | 13.33 | 13.33 | 0.00 | 0.00 | 51.67 | approve |
| FC-TRAINING-WAIVER-115 | 79.99 | 59.99 | 0 | 150 | 13.33 | 13.33 | 0.00 | 0.00 | 136.67 | approve |
| FC-TRAINING-WAIVER-116 | 79.99 | 59.99 | 0 | 350 | 13.33 | 13.33 | 0.00 | 0.00 | 336.67 | approve |
| FC-TRAINING-WAIVER-117 | 79.99 | 59.99 | 8.00 | 12.50 | 13.33 | 5.33 | 0.00 | 0.00 | 7.17 | approve |
| FC-TRAINING-WAIVER-118 | 79.99 | 59.99 | 8.00 | 65 | 13.33 | 5.33 | 0.00 | 0.00 | 59.67 | approve |
| FC-TRAINING-WAIVER-119 | 79.99 | 59.99 | 8.00 | 150 | 13.33 | 5.33 | 0.00 | 0.00 | 144.67 | approve |
| FC-TRAINING-WAIVER-120 | 79.99 | 59.99 | 8.00 | 350 | 13.33 | 5.33 | 0.00 | 0.00 | 344.67 | approve |
| FC-TRAINING-WAIVER-121 | 79.99 | 59.99 | 36.00 | 12.50 | 13.33 | 0.00 | 22.67 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-122 | 79.99 | 59.99 | 36.00 | 65 | 13.33 | 0.00 | 22.67 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-123 | 79.99 | 59.99 | 36.00 | 150 | 13.33 | 0.00 | 22.67 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-124 | 79.99 | 59.99 | 36.00 | 350 | 13.33 | 0.00 | 22.67 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-125 | 79.99 | 59.99 | 63.99 | 12.50 | 13.33 | 0.00 | 50.66 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-126 | 79.99 | 59.99 | 63.99 | 65 | 13.33 | 0.00 | 50.66 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-127 | 79.99 | 59.99 | 63.99 | 150 | 13.33 | 0.00 | 50.66 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-128 | 79.99 | 59.99 | 63.99 | 350 | 13.33 | 0.00 | 50.66 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-129 | 125 | 0.00 | 0 | 12.50 | 83.33 | 12.50 | 0.00 | 70.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-130 | 125 | 0.00 | 0 | 65 | 83.33 | 65.00 | 0.00 | 18.33 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-131 | 125 | 0.00 | 0 | 150 | 83.33 | 83.33 | 0.00 | 0.00 | 66.67 | approve |
| FC-TRAINING-WAIVER-132 | 125 | 0.00 | 0 | 350 | 83.33 | 83.33 | 0.00 | 0.00 | 266.67 | approve |
| FC-TRAINING-WAIVER-133 | 125 | 0.00 | 12.50 | 12.50 | 83.33 | 12.50 | 0.00 | 58.33 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-134 | 125 | 0.00 | 12.50 | 65 | 83.33 | 65.00 | 0.00 | 5.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-135 | 125 | 0.00 | 12.50 | 150 | 83.33 | 70.83 | 0.00 | 0.00 | 79.17 | approve |
| FC-TRAINING-WAIVER-136 | 125 | 0.00 | 12.50 | 350 | 83.33 | 70.83 | 0.00 | 0.00 | 279.17 | approve |
| FC-TRAINING-WAIVER-137 | 125 | 0.00 | 56.25 | 12.50 | 83.33 | 12.50 | 0.00 | 14.58 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-138 | 125 | 0.00 | 56.25 | 65 | 83.33 | 27.08 | 0.00 | 0.00 | 37.92 | approve |
| FC-TRAINING-WAIVER-139 | 125 | 0.00 | 56.25 | 150 | 83.33 | 27.08 | 0.00 | 0.00 | 122.92 | approve |
| FC-TRAINING-WAIVER-140 | 125 | 0.00 | 56.25 | 350 | 83.33 | 27.08 | 0.00 | 0.00 | 322.92 | approve |
| FC-TRAINING-WAIVER-141 | 125 | 0.00 | 100.00 | 12.50 | 83.33 | 0.00 | 16.67 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-142 | 125 | 0.00 | 100.00 | 65 | 83.33 | 0.00 | 16.67 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-143 | 125 | 0.00 | 100.00 | 150 | 83.33 | 0.00 | 16.67 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-144 | 125 | 0.00 | 100.00 | 350 | 83.33 | 0.00 | 16.67 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-145 | 125 | 15.63 | 0 | 12.50 | 72.91 | 12.50 | 0.00 | 60.41 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-146 | 125 | 15.63 | 0 | 65 | 72.91 | 65.00 | 0.00 | 7.91 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-147 | 125 | 15.63 | 0 | 150 | 72.91 | 72.91 | 0.00 | 0.00 | 77.09 | approve |
| FC-TRAINING-WAIVER-148 | 125 | 15.63 | 0 | 350 | 72.91 | 72.91 | 0.00 | 0.00 | 277.09 | approve |
| FC-TRAINING-WAIVER-149 | 125 | 15.63 | 12.50 | 12.50 | 72.91 | 12.50 | 0.00 | 47.91 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-150 | 125 | 15.63 | 12.50 | 65 | 72.91 | 60.41 | 0.00 | 0.00 | 4.59 | approve |
| FC-TRAINING-WAIVER-151 | 125 | 15.63 | 12.50 | 150 | 72.91 | 60.41 | 0.00 | 0.00 | 89.59 | approve |
| FC-TRAINING-WAIVER-152 | 125 | 15.63 | 12.50 | 350 | 72.91 | 60.41 | 0.00 | 0.00 | 289.59 | approve |
| FC-TRAINING-WAIVER-153 | 125 | 15.63 | 56.25 | 12.50 | 72.91 | 12.50 | 0.00 | 4.16 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-154 | 125 | 15.63 | 56.25 | 65 | 72.91 | 16.66 | 0.00 | 0.00 | 48.34 | approve |
| FC-TRAINING-WAIVER-155 | 125 | 15.63 | 56.25 | 150 | 72.91 | 16.66 | 0.00 | 0.00 | 133.34 | approve |
| FC-TRAINING-WAIVER-156 | 125 | 15.63 | 56.25 | 350 | 72.91 | 16.66 | 0.00 | 0.00 | 333.34 | approve |
| FC-TRAINING-WAIVER-157 | 125 | 15.63 | 100.00 | 12.50 | 72.91 | 0.00 | 27.09 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-158 | 125 | 15.63 | 100.00 | 65 | 72.91 | 0.00 | 27.09 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-159 | 125 | 15.63 | 100.00 | 150 | 72.91 | 0.00 | 27.09 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-160 | 125 | 15.63 | 100.00 | 350 | 72.91 | 0.00 | 27.09 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-161 | 125 | 41.25 | 0 | 12.50 | 55.83 | 12.50 | 0.00 | 43.33 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-162 | 125 | 41.25 | 0 | 65 | 55.83 | 55.83 | 0.00 | 0.00 | 9.17 | approve |
| FC-TRAINING-WAIVER-163 | 125 | 41.25 | 0 | 150 | 55.83 | 55.83 | 0.00 | 0.00 | 94.17 | approve |
| FC-TRAINING-WAIVER-164 | 125 | 41.25 | 0 | 350 | 55.83 | 55.83 | 0.00 | 0.00 | 294.17 | approve |
| FC-TRAINING-WAIVER-165 | 125 | 41.25 | 12.50 | 12.50 | 55.83 | 12.50 | 0.00 | 30.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-166 | 125 | 41.25 | 12.50 | 65 | 55.83 | 43.33 | 0.00 | 0.00 | 21.67 | approve |
| FC-TRAINING-WAIVER-167 | 125 | 41.25 | 12.50 | 150 | 55.83 | 43.33 | 0.00 | 0.00 | 106.67 | approve |
| FC-TRAINING-WAIVER-168 | 125 | 41.25 | 12.50 | 350 | 55.83 | 43.33 | 0.00 | 0.00 | 306.67 | approve |
| FC-TRAINING-WAIVER-169 | 125 | 41.25 | 56.25 | 12.50 | 55.83 | 0.00 | 0.42 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-170 | 125 | 41.25 | 56.25 | 65 | 55.83 | 0.00 | 0.42 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-171 | 125 | 41.25 | 56.25 | 150 | 55.83 | 0.00 | 0.42 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-172 | 125 | 41.25 | 56.25 | 350 | 55.83 | 0.00 | 0.42 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-173 | 125 | 41.25 | 100.00 | 12.50 | 55.83 | 0.00 | 44.17 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-174 | 125 | 41.25 | 100.00 | 65 | 55.83 | 0.00 | 44.17 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-175 | 125 | 41.25 | 100.00 | 150 | 55.83 | 0.00 | 44.17 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-176 | 125 | 41.25 | 100.00 | 350 | 55.83 | 0.00 | 44.17 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-177 | 125 | 93.75 | 0 | 12.50 | 20.83 | 12.50 | 0.00 | 8.33 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-178 | 125 | 93.75 | 0 | 65 | 20.83 | 20.83 | 0.00 | 0.00 | 44.17 | approve |
| FC-TRAINING-WAIVER-179 | 125 | 93.75 | 0 | 150 | 20.83 | 20.83 | 0.00 | 0.00 | 129.17 | approve |
| FC-TRAINING-WAIVER-180 | 125 | 93.75 | 0 | 350 | 20.83 | 20.83 | 0.00 | 0.00 | 329.17 | approve |
| FC-TRAINING-WAIVER-181 | 125 | 93.75 | 12.50 | 12.50 | 20.83 | 8.33 | 0.00 | 0.00 | 4.17 | approve |
| FC-TRAINING-WAIVER-182 | 125 | 93.75 | 12.50 | 65 | 20.83 | 8.33 | 0.00 | 0.00 | 56.67 | approve |
| FC-TRAINING-WAIVER-183 | 125 | 93.75 | 12.50 | 150 | 20.83 | 8.33 | 0.00 | 0.00 | 141.67 | approve |
| FC-TRAINING-WAIVER-184 | 125 | 93.75 | 12.50 | 350 | 20.83 | 8.33 | 0.00 | 0.00 | 341.67 | approve |
| FC-TRAINING-WAIVER-185 | 125 | 93.75 | 56.25 | 12.50 | 20.83 | 0.00 | 35.42 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-186 | 125 | 93.75 | 56.25 | 65 | 20.83 | 0.00 | 35.42 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-187 | 125 | 93.75 | 56.25 | 150 | 20.83 | 0.00 | 35.42 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-188 | 125 | 93.75 | 56.25 | 350 | 20.83 | 0.00 | 35.42 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-189 | 125 | 93.75 | 100.00 | 12.50 | 20.83 | 0.00 | 79.17 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-190 | 125 | 93.75 | 100.00 | 65 | 20.83 | 0.00 | 79.17 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-191 | 125 | 93.75 | 100.00 | 150 | 20.83 | 0.00 | 79.17 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-192 | 125 | 93.75 | 100.00 | 350 | 20.83 | 0.00 | 79.17 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-193 | 167.83 | 0.00 | 0 | 12.50 | 111.89 | 12.50 | 0.00 | 99.39 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-194 | 167.83 | 0.00 | 0 | 65 | 111.89 | 65.00 | 0.00 | 46.89 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-195 | 167.83 | 0.00 | 0 | 150 | 111.89 | 111.89 | 0.00 | 0.00 | 38.11 | approve |
| FC-TRAINING-WAIVER-196 | 167.83 | 0.00 | 0 | 350 | 111.89 | 111.89 | 0.00 | 0.00 | 238.11 | approve |
| FC-TRAINING-WAIVER-197 | 167.83 | 0.00 | 16.78 | 12.50 | 111.89 | 12.50 | 0.00 | 82.61 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-198 | 167.83 | 0.00 | 16.78 | 65 | 111.89 | 65.00 | 0.00 | 30.11 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-199 | 167.83 | 0.00 | 16.78 | 150 | 111.89 | 95.11 | 0.00 | 0.00 | 54.89 | approve |
| FC-TRAINING-WAIVER-200 | 167.83 | 0.00 | 16.78 | 350 | 111.89 | 95.11 | 0.00 | 0.00 | 254.89 | approve |
| FC-TRAINING-WAIVER-201 | 167.83 | 0.00 | 75.52 | 12.50 | 111.89 | 12.50 | 0.00 | 23.87 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-202 | 167.83 | 0.00 | 75.52 | 65 | 111.89 | 36.37 | 0.00 | 0.00 | 28.63 | approve |
| FC-TRAINING-WAIVER-203 | 167.83 | 0.00 | 75.52 | 150 | 111.89 | 36.37 | 0.00 | 0.00 | 113.63 | approve |
| FC-TRAINING-WAIVER-204 | 167.83 | 0.00 | 75.52 | 350 | 111.89 | 36.37 | 0.00 | 0.00 | 313.63 | approve |
| FC-TRAINING-WAIVER-205 | 167.83 | 0.00 | 134.26 | 12.50 | 111.89 | 0.00 | 22.37 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-206 | 167.83 | 0.00 | 134.26 | 65 | 111.89 | 0.00 | 22.37 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-207 | 167.83 | 0.00 | 134.26 | 150 | 111.89 | 0.00 | 22.37 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-208 | 167.83 | 0.00 | 134.26 | 350 | 111.89 | 0.00 | 22.37 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-209 | 167.83 | 20.98 | 0 | 12.50 | 97.90 | 12.50 | 0.00 | 85.40 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-210 | 167.83 | 20.98 | 0 | 65 | 97.90 | 65.00 | 0.00 | 32.90 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-211 | 167.83 | 20.98 | 0 | 150 | 97.90 | 97.90 | 0.00 | 0.00 | 52.10 | approve |
| FC-TRAINING-WAIVER-212 | 167.83 | 20.98 | 0 | 350 | 97.90 | 97.90 | 0.00 | 0.00 | 252.10 | approve |
| FC-TRAINING-WAIVER-213 | 167.83 | 20.98 | 16.78 | 12.50 | 97.90 | 12.50 | 0.00 | 68.62 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-214 | 167.83 | 20.98 | 16.78 | 65 | 97.90 | 65.00 | 0.00 | 16.12 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-215 | 167.83 | 20.98 | 16.78 | 150 | 97.90 | 81.12 | 0.00 | 0.00 | 68.88 | approve |
| FC-TRAINING-WAIVER-216 | 167.83 | 20.98 | 16.78 | 350 | 97.90 | 81.12 | 0.00 | 0.00 | 268.88 | approve |
| FC-TRAINING-WAIVER-217 | 167.83 | 20.98 | 75.52 | 12.50 | 97.90 | 12.50 | 0.00 | 9.88 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-218 | 167.83 | 20.98 | 75.52 | 65 | 97.90 | 22.38 | 0.00 | 0.00 | 42.62 | approve |
| FC-TRAINING-WAIVER-219 | 167.83 | 20.98 | 75.52 | 150 | 97.90 | 22.38 | 0.00 | 0.00 | 127.62 | approve |
| FC-TRAINING-WAIVER-220 | 167.83 | 20.98 | 75.52 | 350 | 97.90 | 22.38 | 0.00 | 0.00 | 327.62 | approve |
| FC-TRAINING-WAIVER-221 | 167.83 | 20.98 | 134.26 | 12.50 | 97.90 | 0.00 | 36.36 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-222 | 167.83 | 20.98 | 134.26 | 65 | 97.90 | 0.00 | 36.36 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-223 | 167.83 | 20.98 | 134.26 | 150 | 97.90 | 0.00 | 36.36 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-224 | 167.83 | 20.98 | 134.26 | 350 | 97.90 | 0.00 | 36.36 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-225 | 167.83 | 55.38 | 0 | 12.50 | 74.97 | 12.50 | 0.00 | 62.47 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-226 | 167.83 | 55.38 | 0 | 65 | 74.97 | 65.00 | 0.00 | 9.97 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-227 | 167.83 | 55.38 | 0 | 150 | 74.97 | 74.97 | 0.00 | 0.00 | 75.03 | approve |
| FC-TRAINING-WAIVER-228 | 167.83 | 55.38 | 0 | 350 | 74.97 | 74.97 | 0.00 | 0.00 | 275.03 | approve |
| FC-TRAINING-WAIVER-229 | 167.83 | 55.38 | 16.78 | 12.50 | 74.97 | 12.50 | 0.00 | 45.69 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-230 | 167.83 | 55.38 | 16.78 | 65 | 74.97 | 58.19 | 0.00 | 0.00 | 6.81 | approve |
| FC-TRAINING-WAIVER-231 | 167.83 | 55.38 | 16.78 | 150 | 74.97 | 58.19 | 0.00 | 0.00 | 91.81 | approve |
| FC-TRAINING-WAIVER-232 | 167.83 | 55.38 | 16.78 | 350 | 74.97 | 58.19 | 0.00 | 0.00 | 291.81 | approve |
| FC-TRAINING-WAIVER-233 | 167.83 | 55.38 | 75.52 | 12.50 | 74.97 | 0.00 | 0.55 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-234 | 167.83 | 55.38 | 75.52 | 65 | 74.97 | 0.00 | 0.55 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-235 | 167.83 | 55.38 | 75.52 | 150 | 74.97 | 0.00 | 0.55 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-236 | 167.83 | 55.38 | 75.52 | 350 | 74.97 | 0.00 | 0.55 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-237 | 167.83 | 55.38 | 134.26 | 12.50 | 74.97 | 0.00 | 59.29 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-238 | 167.83 | 55.38 | 134.26 | 65 | 74.97 | 0.00 | 59.29 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-239 | 167.83 | 55.38 | 134.26 | 150 | 74.97 | 0.00 | 59.29 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-240 | 167.83 | 55.38 | 134.26 | 350 | 74.97 | 0.00 | 59.29 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-241 | 167.83 | 125.87 | 0 | 12.50 | 27.97 | 12.50 | 0.00 | 15.47 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-242 | 167.83 | 125.87 | 0 | 65 | 27.97 | 27.97 | 0.00 | 0.00 | 37.03 | approve |
| FC-TRAINING-WAIVER-243 | 167.83 | 125.87 | 0 | 150 | 27.97 | 27.97 | 0.00 | 0.00 | 122.03 | approve |
| FC-TRAINING-WAIVER-244 | 167.83 | 125.87 | 0 | 350 | 27.97 | 27.97 | 0.00 | 0.00 | 322.03 | approve |
| FC-TRAINING-WAIVER-245 | 167.83 | 125.87 | 16.78 | 12.50 | 27.97 | 11.19 | 0.00 | 0.00 | 1.31 | approve |
| FC-TRAINING-WAIVER-246 | 167.83 | 125.87 | 16.78 | 65 | 27.97 | 11.19 | 0.00 | 0.00 | 53.81 | approve |
| FC-TRAINING-WAIVER-247 | 167.83 | 125.87 | 16.78 | 150 | 27.97 | 11.19 | 0.00 | 0.00 | 138.81 | approve |
| FC-TRAINING-WAIVER-248 | 167.83 | 125.87 | 16.78 | 350 | 27.97 | 11.19 | 0.00 | 0.00 | 338.81 | approve |
| FC-TRAINING-WAIVER-249 | 167.83 | 125.87 | 75.52 | 12.50 | 27.97 | 0.00 | 47.55 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-250 | 167.83 | 125.87 | 75.52 | 65 | 27.97 | 0.00 | 47.55 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-251 | 167.83 | 125.87 | 75.52 | 150 | 27.97 | 0.00 | 47.55 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-252 | 167.83 | 125.87 | 75.52 | 350 | 27.97 | 0.00 | 47.55 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-253 | 167.83 | 125.87 | 134.26 | 12.50 | 27.97 | 0.00 | 106.29 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-254 | 167.83 | 125.87 | 134.26 | 65 | 27.97 | 0.00 | 106.29 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-255 | 167.83 | 125.87 | 134.26 | 150 | 27.97 | 0.00 | 106.29 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-256 | 167.83 | 125.87 | 134.26 | 350 | 27.97 | 0.00 | 106.29 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-257 | 320 | 0.00 | 0 | 12.50 | 150.00 | 12.50 | 0.00 | 137.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-258 | 320 | 0.00 | 0 | 65 | 150.00 | 65.00 | 0.00 | 85.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-259 | 320 | 0.00 | 0 | 150 | 150.00 | 150.00 | 0.00 | 0.00 | 0.00 | approve |
| FC-TRAINING-WAIVER-260 | 320 | 0.00 | 0 | 350 | 150.00 | 150.00 | 0.00 | 0.00 | 200.00 | approve |
| FC-TRAINING-WAIVER-261 | 320 | 0.00 | 32.00 | 12.50 | 150.00 | 12.50 | 0.00 | 105.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-262 | 320 | 0.00 | 32.00 | 65 | 150.00 | 65.00 | 0.00 | 53.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-263 | 320 | 0.00 | 32.00 | 150 | 150.00 | 118.00 | 0.00 | 0.00 | 32.00 | approve |
| FC-TRAINING-WAIVER-264 | 320 | 0.00 | 32.00 | 350 | 150.00 | 118.00 | 0.00 | 0.00 | 232.00 | approve |
| FC-TRAINING-WAIVER-265 | 320 | 0.00 | 144.00 | 12.50 | 150.00 | 6.00 | 0.00 | 0.00 | 6.50 | approve |
| FC-TRAINING-WAIVER-266 | 320 | 0.00 | 144.00 | 65 | 150.00 | 6.00 | 0.00 | 0.00 | 59.00 | approve |
| FC-TRAINING-WAIVER-267 | 320 | 0.00 | 144.00 | 150 | 150.00 | 6.00 | 0.00 | 0.00 | 144.00 | approve |
| FC-TRAINING-WAIVER-268 | 320 | 0.00 | 144.00 | 350 | 150.00 | 6.00 | 0.00 | 0.00 | 344.00 | approve |
| FC-TRAINING-WAIVER-269 | 320 | 0.00 | 256.00 | 12.50 | 150.00 | 0.00 | 106.00 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-270 | 320 | 0.00 | 256.00 | 65 | 150.00 | 0.00 | 106.00 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-271 | 320 | 0.00 | 256.00 | 150 | 150.00 | 0.00 | 106.00 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-272 | 320 | 0.00 | 256.00 | 350 | 150.00 | 0.00 | 106.00 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-273 | 320 | 40.00 | 0 | 12.50 | 150.00 | 12.50 | 0.00 | 137.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-274 | 320 | 40.00 | 0 | 65 | 150.00 | 65.00 | 0.00 | 85.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-275 | 320 | 40.00 | 0 | 150 | 150.00 | 150.00 | 0.00 | 0.00 | 0.00 | approve |
| FC-TRAINING-WAIVER-276 | 320 | 40.00 | 0 | 350 | 150.00 | 150.00 | 0.00 | 0.00 | 200.00 | approve |
| FC-TRAINING-WAIVER-277 | 320 | 40.00 | 32.00 | 12.50 | 150.00 | 12.50 | 0.00 | 105.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-278 | 320 | 40.00 | 32.00 | 65 | 150.00 | 65.00 | 0.00 | 53.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-279 | 320 | 40.00 | 32.00 | 150 | 150.00 | 118.00 | 0.00 | 0.00 | 32.00 | approve |
| FC-TRAINING-WAIVER-280 | 320 | 40.00 | 32.00 | 350 | 150.00 | 118.00 | 0.00 | 0.00 | 232.00 | approve |
| FC-TRAINING-WAIVER-281 | 320 | 40.00 | 144.00 | 12.50 | 150.00 | 6.00 | 0.00 | 0.00 | 6.50 | approve |
| FC-TRAINING-WAIVER-282 | 320 | 40.00 | 144.00 | 65 | 150.00 | 6.00 | 0.00 | 0.00 | 59.00 | approve |
| FC-TRAINING-WAIVER-283 | 320 | 40.00 | 144.00 | 150 | 150.00 | 6.00 | 0.00 | 0.00 | 144.00 | approve |
| FC-TRAINING-WAIVER-284 | 320 | 40.00 | 144.00 | 350 | 150.00 | 6.00 | 0.00 | 0.00 | 344.00 | approve |
| FC-TRAINING-WAIVER-285 | 320 | 40.00 | 256.00 | 12.50 | 150.00 | 0.00 | 106.00 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-286 | 320 | 40.00 | 256.00 | 65 | 150.00 | 0.00 | 106.00 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-287 | 320 | 40.00 | 256.00 | 150 | 150.00 | 0.00 | 106.00 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-288 | 320 | 40.00 | 256.00 | 350 | 150.00 | 0.00 | 106.00 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-289 | 320 | 105.60 | 0 | 12.50 | 142.93 | 12.50 | 0.00 | 130.43 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-290 | 320 | 105.60 | 0 | 65 | 142.93 | 65.00 | 0.00 | 77.93 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-291 | 320 | 105.60 | 0 | 150 | 142.93 | 142.93 | 0.00 | 0.00 | 7.07 | approve |
| FC-TRAINING-WAIVER-292 | 320 | 105.60 | 0 | 350 | 142.93 | 142.93 | 0.00 | 0.00 | 207.07 | approve |
| FC-TRAINING-WAIVER-293 | 320 | 105.60 | 32.00 | 12.50 | 142.93 | 12.50 | 0.00 | 98.43 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-294 | 320 | 105.60 | 32.00 | 65 | 142.93 | 65.00 | 0.00 | 45.93 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-295 | 320 | 105.60 | 32.00 | 150 | 142.93 | 110.93 | 0.00 | 0.00 | 39.07 | approve |
| FC-TRAINING-WAIVER-296 | 320 | 105.60 | 32.00 | 350 | 142.93 | 110.93 | 0.00 | 0.00 | 239.07 | approve |
| FC-TRAINING-WAIVER-297 | 320 | 105.60 | 144.00 | 12.50 | 142.93 | 0.00 | 1.07 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-298 | 320 | 105.60 | 144.00 | 65 | 142.93 | 0.00 | 1.07 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-299 | 320 | 105.60 | 144.00 | 150 | 142.93 | 0.00 | 1.07 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-300 | 320 | 105.60 | 144.00 | 350 | 142.93 | 0.00 | 1.07 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-301 | 320 | 105.60 | 256.00 | 12.50 | 142.93 | 0.00 | 113.07 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-302 | 320 | 105.60 | 256.00 | 65 | 142.93 | 0.00 | 113.07 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-303 | 320 | 105.60 | 256.00 | 150 | 142.93 | 0.00 | 113.07 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-304 | 320 | 105.60 | 256.00 | 350 | 142.93 | 0.00 | 113.07 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-305 | 320 | 240.00 | 0 | 12.50 | 53.33 | 12.50 | 0.00 | 40.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-306 | 320 | 240.00 | 0 | 65 | 53.33 | 53.33 | 0.00 | 0.00 | 11.67 | approve |
| FC-TRAINING-WAIVER-307 | 320 | 240.00 | 0 | 150 | 53.33 | 53.33 | 0.00 | 0.00 | 96.67 | approve |
| FC-TRAINING-WAIVER-308 | 320 | 240.00 | 0 | 350 | 53.33 | 53.33 | 0.00 | 0.00 | 296.67 | approve |
| FC-TRAINING-WAIVER-309 | 320 | 240.00 | 32.00 | 12.50 | 53.33 | 12.50 | 0.00 | 8.83 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-310 | 320 | 240.00 | 32.00 | 65 | 53.33 | 21.33 | 0.00 | 0.00 | 43.67 | approve |
| FC-TRAINING-WAIVER-311 | 320 | 240.00 | 32.00 | 150 | 53.33 | 21.33 | 0.00 | 0.00 | 128.67 | approve |
| FC-TRAINING-WAIVER-312 | 320 | 240.00 | 32.00 | 350 | 53.33 | 21.33 | 0.00 | 0.00 | 328.67 | approve |
| FC-TRAINING-WAIVER-313 | 320 | 240.00 | 144.00 | 12.50 | 53.33 | 0.00 | 90.67 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-314 | 320 | 240.00 | 144.00 | 65 | 53.33 | 0.00 | 90.67 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-315 | 320 | 240.00 | 144.00 | 150 | 53.33 | 0.00 | 90.67 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-316 | 320 | 240.00 | 144.00 | 350 | 53.33 | 0.00 | 90.67 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-317 | 320 | 240.00 | 256.00 | 12.50 | 53.33 | 0.00 | 202.67 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-318 | 320 | 240.00 | 256.00 | 65 | 53.33 | 0.00 | 202.67 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-319 | 320 | 240.00 | 256.00 | 150 | 53.33 | 0.00 | 202.67 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-320 | 320 | 240.00 | 256.00 | 350 | 53.33 | 0.00 | 202.67 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-321 | 725.50 | 0.00 | 0 | 12.50 | 150.00 | 12.50 | 0.00 | 137.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-322 | 725.50 | 0.00 | 0 | 65 | 150.00 | 65.00 | 0.00 | 85.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-323 | 725.50 | 0.00 | 0 | 150 | 150.00 | 150.00 | 0.00 | 0.00 | 0.00 | approve |
| FC-TRAINING-WAIVER-324 | 725.50 | 0.00 | 0 | 350 | 150.00 | 150.00 | 0.00 | 0.00 | 200.00 | approve |
| FC-TRAINING-WAIVER-325 | 725.50 | 0.00 | 72.55 | 12.50 | 150.00 | 12.50 | 0.00 | 64.95 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-326 | 725.50 | 0.00 | 72.55 | 65 | 150.00 | 65.00 | 0.00 | 12.45 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-327 | 725.50 | 0.00 | 72.55 | 150 | 150.00 | 77.45 | 0.00 | 0.00 | 72.55 | approve |
| FC-TRAINING-WAIVER-328 | 725.50 | 0.00 | 72.55 | 350 | 150.00 | 77.45 | 0.00 | 0.00 | 272.55 | approve |
| FC-TRAINING-WAIVER-329 | 725.50 | 0.00 | 326.48 | 12.50 | 150.00 | 0.00 | 176.48 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-330 | 725.50 | 0.00 | 326.48 | 65 | 150.00 | 0.00 | 176.48 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-331 | 725.50 | 0.00 | 326.48 | 150 | 150.00 | 0.00 | 176.48 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-332 | 725.50 | 0.00 | 326.48 | 350 | 150.00 | 0.00 | 176.48 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-333 | 725.50 | 0.00 | 580.40 | 12.50 | 150.00 | 0.00 | 430.40 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-334 | 725.50 | 0.00 | 580.40 | 65 | 150.00 | 0.00 | 430.40 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-335 | 725.50 | 0.00 | 580.40 | 150 | 150.00 | 0.00 | 430.40 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-336 | 725.50 | 0.00 | 580.40 | 350 | 150.00 | 0.00 | 430.40 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-337 | 725.50 | 90.69 | 0 | 12.50 | 150.00 | 12.50 | 0.00 | 137.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-338 | 725.50 | 90.69 | 0 | 65 | 150.00 | 65.00 | 0.00 | 85.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-339 | 725.50 | 90.69 | 0 | 150 | 150.00 | 150.00 | 0.00 | 0.00 | 0.00 | approve |
| FC-TRAINING-WAIVER-340 | 725.50 | 90.69 | 0 | 350 | 150.00 | 150.00 | 0.00 | 0.00 | 200.00 | approve |
| FC-TRAINING-WAIVER-341 | 725.50 | 90.69 | 72.55 | 12.50 | 150.00 | 12.50 | 0.00 | 64.95 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-342 | 725.50 | 90.69 | 72.55 | 65 | 150.00 | 65.00 | 0.00 | 12.45 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-343 | 725.50 | 90.69 | 72.55 | 150 | 150.00 | 77.45 | 0.00 | 0.00 | 72.55 | approve |
| FC-TRAINING-WAIVER-344 | 725.50 | 90.69 | 72.55 | 350 | 150.00 | 77.45 | 0.00 | 0.00 | 272.55 | approve |
| FC-TRAINING-WAIVER-345 | 725.50 | 90.69 | 326.48 | 12.50 | 150.00 | 0.00 | 176.48 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-346 | 725.50 | 90.69 | 326.48 | 65 | 150.00 | 0.00 | 176.48 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-347 | 725.50 | 90.69 | 326.48 | 150 | 150.00 | 0.00 | 176.48 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-348 | 725.50 | 90.69 | 326.48 | 350 | 150.00 | 0.00 | 176.48 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-349 | 725.50 | 90.69 | 580.40 | 12.50 | 150.00 | 0.00 | 430.40 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-350 | 725.50 | 90.69 | 580.40 | 65 | 150.00 | 0.00 | 430.40 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-351 | 725.50 | 90.69 | 580.40 | 150 | 150.00 | 0.00 | 430.40 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-352 | 725.50 | 90.69 | 580.40 | 350 | 150.00 | 0.00 | 430.40 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-353 | 725.50 | 239.42 | 0 | 12.50 | 150.00 | 12.50 | 0.00 | 137.50 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-354 | 725.50 | 239.42 | 0 | 65 | 150.00 | 65.00 | 0.00 | 85.00 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-355 | 725.50 | 239.42 | 0 | 150 | 150.00 | 150.00 | 0.00 | 0.00 | 0.00 | approve |
| FC-TRAINING-WAIVER-356 | 725.50 | 239.42 | 0 | 350 | 150.00 | 150.00 | 0.00 | 0.00 | 200.00 | approve |
| FC-TRAINING-WAIVER-357 | 725.50 | 239.42 | 72.55 | 12.50 | 150.00 | 12.50 | 0.00 | 64.95 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-358 | 725.50 | 239.42 | 72.55 | 65 | 150.00 | 65.00 | 0.00 | 12.45 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-359 | 725.50 | 239.42 | 72.55 | 150 | 150.00 | 77.45 | 0.00 | 0.00 | 72.55 | approve |
| FC-TRAINING-WAIVER-360 | 725.50 | 239.42 | 72.55 | 350 | 150.00 | 77.45 | 0.00 | 0.00 | 272.55 | approve |
| FC-TRAINING-WAIVER-361 | 725.50 | 239.42 | 326.48 | 12.50 | 150.00 | 0.00 | 176.48 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-362 | 725.50 | 239.42 | 326.48 | 65 | 150.00 | 0.00 | 176.48 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-363 | 725.50 | 239.42 | 326.48 | 150 | 150.00 | 0.00 | 176.48 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-364 | 725.50 | 239.42 | 326.48 | 350 | 150.00 | 0.00 | 176.48 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-365 | 725.50 | 239.42 | 580.40 | 12.50 | 150.00 | 0.00 | 430.40 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-366 | 725.50 | 239.42 | 580.40 | 65 | 150.00 | 0.00 | 430.40 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-367 | 725.50 | 239.42 | 580.40 | 150 | 150.00 | 0.00 | 430.40 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-368 | 725.50 | 239.42 | 580.40 | 350 | 150.00 | 0.00 | 430.40 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-369 | 725.50 | 544.13 | 0 | 12.50 | 120.91 | 12.50 | 0.00 | 108.41 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-370 | 725.50 | 544.13 | 0 | 65 | 120.91 | 65.00 | 0.00 | 55.91 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-371 | 725.50 | 544.13 | 0 | 150 | 120.91 | 120.91 | 0.00 | 0.00 | 29.09 | approve |
| FC-TRAINING-WAIVER-372 | 725.50 | 544.13 | 0 | 350 | 120.91 | 120.91 | 0.00 | 0.00 | 229.09 | approve |
| FC-TRAINING-WAIVER-373 | 725.50 | 544.13 | 72.55 | 12.50 | 120.91 | 12.50 | 0.00 | 35.86 | 0.00 | ceiling reached |
| FC-TRAINING-WAIVER-374 | 725.50 | 544.13 | 72.55 | 65 | 120.91 | 48.36 | 0.00 | 0.00 | 16.64 | approve |
| FC-TRAINING-WAIVER-375 | 725.50 | 544.13 | 72.55 | 150 | 120.91 | 48.36 | 0.00 | 0.00 | 101.64 | approve |
| FC-TRAINING-WAIVER-376 | 725.50 | 544.13 | 72.55 | 350 | 120.91 | 48.36 | 0.00 | 0.00 | 301.64 | approve |
| FC-TRAINING-WAIVER-377 | 725.50 | 544.13 | 326.48 | 12.50 | 120.91 | 0.00 | 205.57 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-378 | 725.50 | 544.13 | 326.48 | 65 | 120.91 | 0.00 | 205.57 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-379 | 725.50 | 544.13 | 326.48 | 150 | 120.91 | 0.00 | 205.57 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-380 | 725.50 | 544.13 | 326.48 | 350 | 120.91 | 0.00 | 205.57 | 0.00 | 350.00 | recover |
| FC-TRAINING-WAIVER-381 | 725.50 | 544.13 | 580.40 | 12.50 | 120.91 | 0.00 | 459.49 | 0.00 | 12.50 | recover |
| FC-TRAINING-WAIVER-382 | 725.50 | 544.13 | 580.40 | 65 | 120.91 | 0.00 | 459.49 | 0.00 | 65.00 | recover |
| FC-TRAINING-WAIVER-383 | 725.50 | 544.13 | 580.40 | 150 | 120.91 | 0.00 | 459.49 | 0.00 | 150.00 | recover |
| FC-TRAINING-WAIVER-384 | 725.50 | 544.13 | 580.40 | 350 | 120.91 | 0.00 | 459.49 | 0.00 | 350.00 | recover |

## Reconciliation

Subtract prior claims from cumulative entitlement. A negative result requires a recovery review and never creates a new negative draw. Award remaining decreases exactly by the new claim. Amounts above the remaining award stay visible as unfunded eligible cost. Status alone does not authorize immediate recovery cash.

[Finance decision fixture index](../README.md)
