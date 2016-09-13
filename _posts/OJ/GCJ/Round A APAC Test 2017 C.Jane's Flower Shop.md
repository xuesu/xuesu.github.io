# Problem

Jane plans to open a flower shop in the local flower market. The initial cost includes the booth license, furnishings and decorations, a truck to transport flowers from the greenhouse to the shop, and so on. Jane will have to recoup these costs by earning income. She has estimated how much net income she will earn in each of the following M months.

Jane wants to predict how successful her flower shop will be by calculating the IRR (Internal Rate of Return) for the M-month period. Given a series of (time, cash flow) pairs (i, Ci), the IRR is the compound interest rate that would make total cash exactly 0 at the end of the last month. The higher the IRR is, the more successful the business is. If the IRR is lower than the inflation rate, it would be wise not to start the business in the first place.

For example, suppose the initial cost is $10,000 and the shop runs for 3 months, with net incomes of $3,000, $4,000, and $5,000, respectively. Then the IRR r is given by:



In this case, there is only one rate (~=8.8963%) that satisfies the equation.

Help Jane to calculate the IRR for her business. It is guaranteed that -1 < r < 1, and there is exactly one solution in each test case.

# 题意
求满足等式的r

# 思路
一开始想到使用二分，但是没有想到如何得到单调性

其实可以两边同时除以（1 + r）的m次方，这样c0对应的就成为了常数项

# Code
暂缺