---
                  layout: post
                  title: "[leetcode]Generate Parentheses"
                  description: "leetcode题目Generate Parentheses的算法分析"
                  category: [leetcode]
                  tags: [leetcode]
---
{% include JB/setup %}
#[leetcode]Generate Parentheses
- [题目]

> Generate Parentheses 
> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
> 
> For example, given n = 3, a solution set is:
> 
> "((()))", "(()())", "(())()", "()(())", "()()()"

- [思考]

这题涉及到经典的算法——回溯法。
就以这道题为例子说明一下啥是回溯法(backtracking)吧。
这题求的是所有可能性的集合。回溯法，就是通过递归，去穷尽所有的可能性。每次递归只处理一步，并做条件检验，如果不符合要求，就不会再进行下去；如果处理结束，就将当前这个可能性放在结果集中。
换个方式说，就是顺序执行下面的步骤：


1. 当前的结果是我要的吗？
2. 是。那么好，还需要进一步的处理吗？
3. 是。那么，根据需要进入递归。
4. 在本层递归的结果是我要的吗？是的话，将结果加入结果集。如果需要进一步处理，返回执行3；如果不符合条件，结束执行。

- [代码]
<pre class="prettyprint">
public class Solution {
    public ArrayList<String> generateParenthesis(int n) {
        ArrayList<String> rst = new ArrayList<String>();
        if(n <= 0) {
            return rst;
        }
        getPair(rst, "", n, n);
        return rst;
    }
    
	public void getPair( ArrayList<String> rst , String s, int left, int right) {
		//当前结果不符合要求，退出执行
		if(left > right || left < 0 || right < 0) {
			return; 	
		}
		//符合条件，加入结果集
		if(left == 0 && right == 0) {
			rst.add(s);
			return;
		}
		//每次递归，只处理一步；递归调用，进行进一步的处理。
		getPair(rst, s + "(", left - 1, right);
		getPair(rst, s + ")", left, right - 1);
	}
}
</pre>


