# LeetCode36.有效的数独
## 题目
判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。


1. 数字 1-9 在每一行只能出现一次。
2. 数字 1-9 在每一列只能出现一次。
3. 数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。


![](https://i.imgur.com/zTgxHJx.png)

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 '.' 表示。

## eg1

输入:

	[
	  ["5","3",".",".","7",".",".",".","."],
	  ["6",".",".","1","9","5",".",".","."],
	  [".","9","8",".",".",".",".","6","."],
	  ["8",".",".",".","6",".",".",".","3"],
	  ["4",".",".","8",".","3",".",".","1"],
	  ["7",".",".",".","2",".",".",".","6"],
	  [".","6",".",".",".",".","2","8","."],
	  [".",".",".","4","1","9",".",".","5"],
	  [".",".",".",".","8",".",".","7","9"]
	]

输出: true

## eg2

输入:

	[
	  ["8","3",".",".","7",".",".",".","."],
	  ["6",".",".","1","9","5",".",".","."],
	  [".","9","8",".",".",".",".","6","."],
	  ["8",".",".",".","6",".",".",".","3"],
	  ["4",".",".","8",".","3",".",".","1"],
	  ["7",".",".",".","2",".",".",".","6"],
	  [".","6",".",".",".",".","2","8","."],
	  [".",".",".","4","1","9",".",".","5"],
	  [".",".",".",".","8",".",".","7","9"]
	]

输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。

但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。

## 默认代码模板

	class Solution {
	public:
	    bool isValidSudoku(vector<vector<char>>& board) {
	        
	    }
	};


## 解法

分别按照 行、列、3x3的方式遍历

利用STL 中set 中元素唯一的性质

将非'.'元素加入set集合，判断加入前与加入后集合的长度是否变化

如果变化说明元素未重复

如果未变化说明元素重复

**每遍历一行 一列 一个3x3 都用clear()函数清除集合中的元素**

**利用insert()向集合中插入函数**

**(int)(char-'0')将字符型数字强制转化为整型数字**

**3x3时候，有个小技巧，先找到每个3x3第一个元素的位置，然后向右向下分别遍历3个元素，利用除法结果与余数来定位位置，详见代码**

---

	class Solution {
	public:
	    bool isValidSudoku(vector<vector<char>>& board) {
	        set<int> s;
	        //行
	        for(int i = 0; i < 9; i++)
	        {
	            for(int j = 0; j < 9; j++)
	            {
	                if(board[i][j] != '.') 
	                {
	                    int length = s.size();
	                    s.insert((int)(board[i][j] - '0'));
	                    if(s.size() == length) return false;
	                }
	            }
	            s.clear();
	        }
	        
	        //列
	        for(int j = 0; j < 9; j++)
	        {
	            for(int i = 0; i < 9; i++)
	            {   
	                if(board[i][j] != '.')
	                {
	                    int length = s.size();
	                    s.insert((int)(board[i][j] - '0'));
	                    if(s.size() == length) return false;
	                }
	            }
	            s.clear();
	        }
	        
	        //3 x 3
	        int local = 0;
	        while(local < 9)
	        {
	            int i = local / 3;
	            int j = local % 3;
	            i = i * 3;
	            j = j * 3;
	            int counter = 0;
	            for(int m = 0; m < 3; m++)
	            {
	                for(int n = 0; n < 3; n++)
	                {
	                    if(board[i + m][j + n] != '.')
	                    {
	                        int length = s.size();
	                        s.insert((int)(board[i + m][j + n] - '0'));
	                        if(s.size() == length) return false;
	                    }
	                }
	            }
	            s.clear();
	            local++;
	        }
	        
	        return true;
	    }
	};

---