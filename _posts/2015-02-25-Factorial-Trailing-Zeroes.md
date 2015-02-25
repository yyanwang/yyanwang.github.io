---
                  layout: post
                  title: "[leetcode]Factorial Trailing Zeroes"
                  description: "leetcode题目Factorial Trailing Zeroes的算法分析"
                  category: [leetcode]
                  tags: [leetcode]
---
{% include JB/setup %}

#[leetcode]Factorial Trailing Zeroes 

- [题目]


Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

求n!末尾有几个零。要求时间复杂度是对数级别的。

- [思考]

首先想到的是求出n!然后循环除以10，对10取余数。但是用不了多久结果就溢出了Σ( ° △ °|||)︴ 

于是转换角度。

10分解质因数只能是2*5.

显然n!质因数2要比5多的多。所以只需要看n!能分解出多少个5。

首先想到的是n次循环，看1到n每个数能分解出几个5，求和。可行不过还是太慢，不合时间复杂度的要求。

能分解出多少个5，然后复杂度还是指数型的。。。

考虑当n是5的倍数，5,10,15,20。。。也就是floor(n/5)个5.

进一步考虑，如果n=25，25是5的平方，分解成5*5，其中一个5已经算在floor(n/5)当中了，所以结果是floor(n/5)+1;如果n==50，结果是floor(n/5)+2....以此类推，结果是floor(n/5)+floor(n/5^2);

再考虑n=5^3,5^4,...最终得出零的个数是：
numberOfZeros=floor(n/5)+floor(n/5^2)+floor(n/5^3)+...直到floor(n/5^x)=0.

- [限制]

目前方案满足题目时间复杂度的要求。

- [实现]

<pre class="prettyprint">
public class Solution {
    public int trailingZeroes(int n) {
		int zeros = 0;
		for(int i=1;n>=Math.pow(5,i);i++){
		    zeros+=Math.floor(n/Math.pow(5,i));
		}
		return zeros;
    }
}
</pre>


- [感想]

看到题目要求指数的时间复杂度时，就应该想到最终的方案的！:(
